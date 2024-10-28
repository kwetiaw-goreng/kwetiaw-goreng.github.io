---
title: Using Microsoft Forms and Logic Apps to Upload Entra ID User Photo
categories:
  - 
tags:
  - 
aliases: 
share: true
---

Create Microsoft Forms with at least 2 questions, you may add some more depending on your requirement

My form only uses 2 questions, UserPrincipalName (Email) and the attachment question

![forms-user-photo-upload.png](/images/forms-user-photo-upload.png)

Here's the designer view of the logic app

![forms_user_photo_upload_la.png](/images/forms_user_photo_upload_la.png)

Here's the code for the logic app, make sure to replace YOUR_SUBSCRIPTION_ID with your own ID.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
   "contentVersion": "1.0.0.0",
   "parameters": {
      "connections_microsoftforms_externalid": {
         "defaultValue": "/subscriptions/b5378d10-37f7-497e-9c9d-8deaef8ae479/resourceGroups/dt-staffphoto-npe/providers/Microsoft.Web/connections/microsoftforms",
         "type": "String"
      },
      "connections_onedriveforbusiness_externalid": {
         "defaultValue": "/subscriptions/b5378d10-37f7-497e-9c9d-8deaef8ae479/resourceGroups/dt-staffphoto-npe/providers/Microsoft.Web/connections/onedriveforbusiness",
         "type": "String"
      },
      "workflows_staff_photo_processor_name": {
         "defaultValue": "staff-photo-processor",
         "type": "String"
      }
   },
   "resources": [
      {
         "apiVersion": "2017-07-01",
         "identity": {
            "type": "SystemAssigned"
         },
         "location": "australiaeast",
         "name": "[parameters('workflows_staff_photo_processor_name')]",
         "properties": {
            "definition": {
               "$schema": "https://schema.management.azure.com/schemas/2016-06-01/workflowdefinition.json#",
               "actions": {
                  "For_each": {
                     "actions": {
                        "Get_file_content_using_path": {
                           "inputs": {
                              "host": {
                                 "connection": {
                                    "name": "@parameters('$connections')['onedriveforbusiness']['connectionId']"
                                 }
                              },
                              "method": "get",
                              "path": "/datasets/default/GetFileContentByPath",
                              "queries": {
                                 "inferContentType": true,
                                 "path": "/Apps/Microsoft Forms/Untitled form/Question/@{item()['name']}"
                              }
                           },
                           "runAfter": {},
                           "type": "ApiConnection"
                        },
                        "Move_or_rename_a_file_using_path": {
                           "inputs": {
                              "host": {
                                 "connection": {
                                    "name": "@parameters('$connections')['onedriveforbusiness']['connectionId']"
                                 }
                              },
                              "method": "post",
                              "path": "/datasets/default/MoveFileByPath",
                              "queries": {
                                 "destination": "/Apps/Microsoft Forms/Untitled form/Question/Processed/@{body('Get_response_details')?['r071a9be464aa43acbe1bb4564a0c4f9f']}",
                                 "overwrite": false,
                                 "source": "/Apps/Microsoft Forms/Untitled form/Question/@{item()['name']}"
                              }
                           },
                           "runAfter": {
                              "Update_Profile_Photo": [
                                 "Succeeded"
                              ]
                           },
                           "type": "ApiConnection"
                        },
                        "Update_Profile_Photo": {
                           "inputs": {
                              "authentication": {
                                 "audience": "https://graph.microsoft.com",
                                 "type": "ManagedServiceIdentity"
                              },
                              "body": "@body('Get_file_content_using_path')",
                              "headers": {
                                 "Content-Type": "image/jpeg"
                              },
                              "method": "PUT",
                              "uri": "https://graph.microsoft.com/v1.0/users/@{body('Get_response_details')?['r071a9be464aa43acbe1bb4564a0c4f9f']}/photo/$value"
                           },
                           "metadata": {
                              "operationMetadataId": "unique-id-1"
                           },
                           "runAfter": {
                              "Get_file_content_using_path": [
                                 "Succeeded"
                              ]
                           },
                           "type": "Http"
                        }
                     },
                     "foreach": "@outputs('Parse_JSON')['body']",
                     "runAfter": {
                        "Parse_JSON": [
                           "Succeeded"
                        ]
                     },
                     "type": "Foreach"
                  },
                  "Get_response_details": {
                     "inputs": {
                        "host": {
                           "connection": {
                              "name": "@parameters('$connections')['microsoftforms']['connectionId']"
                           }
                        },
                        "method": "get",
                        "path": "/formapi/api/forms('@{encodeURIComponent('CVUPtCIUnkyorVw_xfaUW7QSmZD7NCFHs3DqAx-YcTpUNUo2Q1U5WEM3WUVBS1pMOURBRVM3VVpKOS4u')}')/responses",
                        "queries": {
                           "response_id": "@triggerBody()?['resourceData']?['responseId']"
                        }
                     },
                     "runAfter": {},
                     "type": "ApiConnection"
                  },
                  "Parse_JSON": {
                     "inputs": {
                        "content": "@body('Get_response_details')?['rd7884677b3664c1d80b2d39fd9f2a7b3']",
                        "schema": {
                           "items": {
                              "properties": {
                                 "driveId": {
                                    "type": "string"
                                 },
                                 "id": {
                                    "type": "string"
                                 },
                                 "link": {
                                    "type": "string"
                                 },
                                 "name": {
                                    "type": "string"
                                 },
                                 "referenceId": {
                                    "type": "string"
                                 },
                                 "size": {
                                    "type": "integer"
                                 },
                                 "status": {
                                    "type": "integer"
                                 },
                                 "type": {},
                                 "uploadSessionUrl": {}
                              },
                              "required": [
                                 "name",
                                 "link",
                                 "id",
                                 "type",
                                 "size",
                                 "referenceId",
                                 "driveId",
                                 "status",
                                 "uploadSessionUrl"
                              ],
                              "type": "object"
                           },
                           "type": "array"
                        }
                     },
                     "runAfter": {
                        "Get_response_details": [
                           "Succeeded"
                        ]
                     },
                     "type": "ParseJson"
                  }
               },
               "contentVersion": "1.0.0.0",
               "parameters": {
                  "$connections": {
                     "defaultValue": {},
                     "type": "Object"
                  }
               },
               "triggers": {
                  "When_a_new_response_is_submitted": {
                     "inputs": {
                        "body": {
                           "eventType": "responseAdded",
                           "notificationUrl": "@listCallbackUrl()",
                           "source": "ms-connector"
                        },
                        "host": {
                           "connection": {
                              "name": "@parameters('$connections')['microsoftforms']['connectionId']"
                           }
                        },
                        "path": "/formapi/api/forms/@{encodeURIComponent('CVUPtCIUnkyorVw_xfaUW7QSmZD7NCFHs3DqAx-YcTpUNUo2Q1U5WEM3WUVBS1pMOURBRVM3VVpKOS4u')}/webhooks"
                     },
                     "splitOn": "@triggerBody()?['value']",
                     "type": "ApiConnectionWebhook"
                  }
               }
            },
            "parameters": {
               "$connections": {
                  "value": {
                     "microsoftforms": {
                        "connectionId": "[parameters('connections_microsoftforms_externalid')]",
                        "connectionName": "microsoftforms",
                        "id": "/subscriptions/b5378d10-37f7-497e-9c9d-8deaef8ae479/providers/Microsoft.Web/locations/australiaeast/managedApis/microsoftforms"
                     },
                     "onedriveforbusiness": {
                        "connectionId": "[parameters('connections_onedriveforbusiness_externalid')]",
                        "connectionName": "onedriveforbusiness",
                        "id": "/subscriptions/b5378d10-37f7-497e-9c9d-8deaef8ae479/providers/Microsoft.Web/locations/australiaeast/managedApis/onedriveforbusiness"
                     }
                  }
               }
            },
            "state": "Enabled"
         },
         "type": "Microsoft.Logic/workflows"
      }
   ],
   "variables": {}
}
```

Make sure to use Managed Identity for better security and less overhead and it needs at least `User.ReadWrite.All`

It's so easy to extend what the logic app can do after a successful run, you could archive the photo to different folder depending on the outcome of the run, you could add notification to relevant people/team, etc.
