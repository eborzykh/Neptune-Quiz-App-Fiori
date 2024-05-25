# Neptune-Quiz-App-Fiori
This is an optional part of [Neptune-Quiz-App]( https://github.com/eborzykh/Neptune-Quiz-App). 
Below steps will generate SAP Fiori Cockpit application using [Neptune-Quiz-App-CDS](https://github.com/eborzykh/Neptune-Quiz-App-CDS) to visualise backend data and test ABAP CDS View and SAP Fiori integration.

### Creating SAP Fiori application from template
Following key steps below:
- Visual Studio comand: `Fiori: Open Application Generator`
- Template: `List Report Page`
- Data source and service: `ZNEPT_QZ_UI_QUIZ_02 – OData V2`
- Main Entry: `Quiz` Navigation Entry: `to_Parts`
- Minimum SAPUI5 Version: `http://[host]:[port]/sap/public/bc/ui5_ui5/`

The SAP Fiori application is ready for preview:
![](https://github.com/eborzykh/Neptune-Quiz-App-Fiori/blob/main/images/10_Fiori_Page_First.png)

> [!NOTE]
> The data structure in Neptune Quiz App has 4 levels: `Quiz`, `Parts` (optional level), `Questions` and `Variants`.
> In the Template Wizard it was only possible to set one navigation entry. This can be manually changed in `manifest.json` below.

Find the following generated code in `manifest.json` file:
```
  "sap.ui.generic.app": {
    "_version": "1.3.0",
    "settings": {
      "forceGlobalRefresh": false,
      "objectPageHeaderType": "Dynamic",
      "considerAnalyticalParameters": true,
      "showDraftToggle": false
    },
    "pages": {
      "ListReport|Quiz": {
        "entitySet": "Quiz",
        "component": {
          "name": "sap.suite.ui.generic.template.ListReport",
          "list": true,
          "settings": {
            "condensedTableLayout": true,
            "smartVariantManagement": true,
            "enableTableFilterInPageVariant": true,
            "filterSettings": {
              "dateSettings": {
                "useDateRange": true
              }
            }
          }
        },
        "pages": {
          "ObjectPage|Quiz": {
            "entitySet": "Quiz",
            "defaultLayoutTypeIfExternalNavigation": "MidColumnFullScreen",
            "component": {
              "name": "sap.suite.ui.generic.template.ObjectPage"
            },
            "pages": {
              "ObjectPage|to_Parts": {
                "navigationProperty": "to_Parts",
                "entitySet": "Parts",
                "defaultLayoutTypeIfExternalNavigation": "MidColumnFullScreen",
                "component": {
                  "name": "sap.suite.ui.generic.template.ObjectPage"
                },
```
And insert the code below:
```
                "pages": {
                  "ObjectPage|to_Questions": {
                    "navigationProperty": "to_Questions",
                    "entitySet": "Questions",
                    "defaultLayoutTypeIfExternalNavigation": "MidColumnFullScreen",
                    "component": {
                      "name": "sap.suite.ui.generic.template.ObjectPage"
                    },
                    "pages": {
                      "ObjectPage|to_Variants": {
                        "navigationProperty": "to_Variants",
                        "entitySet": "Variants",
                        "defaultLayoutTypeIfExternalNavigation": "MidColumnFullScreen",
                        "component": {
                          "name": "sap.suite.ui.generic.template.ObjectPage"
                        }
                      }
                    }
                  }
                }
              },
              "ObjectPage|to_Questions": {
                "navigationProperty": "to_Questions",
                "entitySet": "Questions",
                "defaultLayoutTypeIfExternalNavigation": "MidColumnFullScreen",
                "component": {
                  "name": "sap.suite.ui.generic.template.ObjectPage"
                },
                "pages": {
                  "ObjectPage|to_Variants": {
                    "navigationProperty": "to_Variants",
                    "entitySet": "Variants",
                    "defaultLayoutTypeIfExternalNavigation": "MidColumnFullScreen",
                    "component": {
                      "name": "sap.suite.ui.generic.template.ObjectPage"
                    }
                  }
                }
```
Until this point.
```
              }
            }
          }
        }
      }
    }
  },
  "sap.fiori": {
    "registrationIds": [],
    "archeType": "transactional"
  }
```

After saving `manifest.json` file all navigation levels will be available.

### Related links:
* Part 1. [Neptune-Quiz-App](https://github.com/eborzykh/Neptune-Quiz-App)
* Part 2. [Neptune-Quiz-App-CDS](https://github.com/eborzykh/Neptune-Quiz-App-CDS)
* Part 3. Neptune-Quiz-App-Fiori
