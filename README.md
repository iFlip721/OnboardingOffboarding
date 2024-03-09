
# Getting Started

**All scripts** within the respository must be run from the root of the **Build** folder. After you have copied the **Build** folder to the root of your Power Platform project, make sure you `cd .\Build` into that folder to execute each function.

Clone repository to your local computer.

`git clone git@gitlab.dcma.mil:sdg/powerapp/BuildScripts.git`

Copy the `Build` folder into the root of your Power Platform project.

> Update the `config.json` file to match the values of your current Power Platform project.

The **`solutionName`** must match exactly as your Power Platform project name. Replace **`<SOLUTION NAME HERE>`** with the name of your solution.

```json
"project": {
    "solutionName": "<SOLUTION NAME HERE>"
}
```

The environment values are already configured for all DCMA basic lower & upper but these values can be redefined or more can be added using the `json` structure.

```json
"env": [
    {
        "id": 1,
        "name": "DCMA_DEV",
        "env_id": "29e06d80-49ea-4b5a-8369-3be0329da8fc"
    },
    {
        "id": 2,
        "name": "DCMA_TEST",
        "env_id": "3ddc5ce7-74d2-43d2-8324-17ba7baf8640"
    },
    {
        "id": 3,
        "name": "DCMA_PROD",
        "env_id": "f9ad359e-3010-42a2-8e91-aa27b4428e44"
    },
    {
        "id": 4,
        "name": "DCMA_CITDEV",
        "env_id": "7d53a00d-09cc-eb21-8348-99a10042d965"
    }
]
```

# Generate Settings File(s)

A settings file will be generated for each environment `env[]` that is configured in `config.json`. The script will automatically generate each settings file with the default blank values and naming convetion to help make build and deploy execution simplified.

### Example syntax
```powershell
.\generateSettingsFile.ps1
```

You can expect the following results to be generated in the root of your Power Platform project when you execute the `.\generateSettingsFile.ps1` script with the default `config.json`.

```shell
dcma_citdev.7d53a00d-09cc-eb21-8348-99a10042d965.json
dcma_dev.29e06d80-49ea-4b5a-8369-3be0329da8fc.json
dcma_test.3ddc5ce7-74d2-43d2-8324-17ba7baf8640.json
dcma_prod.f9ad359e-3010-42a2-8e91-aa27b4428e44.json
```

Each settings file will need to be updated with the appropriate values for each environment - especially if you're using connection references.

# Build Solution Package

Building the solution package will typically always be done from the **DCMA_DEV** environment. By default, when you execute `.\Build.ps1` the **DCMA_DEV** environment is selected by default. If you need to build a soltuion package from a different environment, use the following syntax:

### Example syntax

```powershell
.\Build.ps1
.\Build.ps1 -env DCMA_CITDEV
.\Build.ps1 -env DCMA_TEST
.\Build.ps1 -env DCMA_PROD
```

> The `-env` value has tab completion enabled.

### Example directory structure after build

```shell
📁.
📁Build/
├── build.ps1
├── config.json
├── deploy.ps1
├── generateSettingsFile.ps1
└── publicFuncs.ps1
📁Documentation/
├── 📁Application/
│   └── Groups.txt
└── 📁Schema/
    ├── Flow - composeChecklist.json
    ├── Flow - composeTask.json
    ├── OBOF - ChecklistJSON-Sample.json
    ├── OBOF - ChecklistJSON-Schema-Documented.json
    ├── OBOF - ChecklistJSON-Schema.json
    ├── OBOF - Comments-Sample.json
    ├── OBOF - Comments-Schema.json
    └── OBOF Data Model - USER.svg
📁environmentvariabledefinitions/
├── sdg_GLBLDSappRegistration
├── sdg_GLBLDSuserAppAssociation
├── sdg_GLBLDSuserRegistration
├── sdg_OBOFDSappSettings
├── sdg_OBOFDSchecklistOutProcessing
├── sdg_OBOFDSmandatoryOffices
├── sdg_OBOFDSmandatoryOfficesPOC
├── sdg_OBOFDSmandatoryOfficesUID
├── sdg_OBOFDStemplateOutProcessingChecklist
├── sdg_OBOFDStemplateOutProcessingChecklistLocalTask
├── sdg_OBOFDSuserDelegation
├── sdg_OBOFRepository
└── sdg_OBOFStorageLocationURL
📁Other/
├── Customizations.xml
└── Solution.xml
📁spo-templates/
├── appRegistration.stp
├── OBOF-appSettings.stp
├── OBOF-checklistOutProcessing.stp
├── OBOF-MandatoryOffices.stp
├── OBOF-MandatoryOfficesPOC.stp
├── OBOF-templateOutProcessingChecklist.stp
├── OBOF-templateOutProcessingChecklistLocalTask.stp
├── OBOF-userDelegation.stp
├── userAppAssociation.stp
└── userRegistration.stp
📁TestPlans/
└── TEST SUITE - 001.fx.yaml
📁Workflows/
├── ClearingOffice-Generate-UID-B168BB5E-7577-EE11-9AE5-001DD8105346.json
├── ClearingOffice-Generate-UID-B168BB5E-7577-EE11-9AE5-001DD8105346.json.data.xml
├── mandatoryOfficesPOC-Sync-UID-68155528-228D-EE11-8179-001DD810548E.json
├── mandatoryOfficesPOC-Sync-UID-68155528-228D-EE11-8179-001DD810548E.json.data.xml
├── OBOF-AddUserGroup-71467F39-0BB7-EE11-A569-001DD8105346.json
├── OBOF-AddUserGroup-71467F39-0BB7-EE11-A569-001DD8105346.json.data.xml
├── OBOF-SecurityRoles-Audit-7999123F-1CC4-EE11-9079-001DD810548E.json
├── OBOF-SecurityRoles-Audit-7999123F-1CC4-EE11-9079-001DD810548E.json.data.xml
├── OBOF-SendNotification-744A8EB1-B890-EE11-8179-001DD810548E.json
├── OBOF-SendNotification-744A8EB1-B890-EE11-8179-001DD810548E.json.data.xml
├── OBOF-SendNotification-Comment-BF5D020E-0092-EE11-8179-001DD810548E.json
├── OBOF-SendNotification-Comment-BF5D020E-0092-EE11-8179-001DD810548E.json.data.xml
├── OBOF-SendNotification-SupervisorDesignee-59FF7017-9F98-EE11-BE37-001DD8105346.json
├── OBOF-SendNotification-SupervisorDesignee-59FF7017-9F98-EE11-BE37-001DD8105346.json.data.xml
├── OBOF-SendNotification-WeeklyRollup-Completed-9CFB8478-1E9D-EE11-BE37-001DD810548E.json
├── OBOF-SendNotification-WeeklyRollup-Completed-9CFB8478-1E9D-EE11-BE37-001DD810548E.json.data.xml
├── OBOF-SendNotification-WeeklyRollup-InProgress-8A9B0865-3396-EE11-8179-001DD8105346.json
├── OBOF-SendNotification-WeeklyRollup-InProgress-8A9B0865-3396-EE11-8179-001DD8105346.json.data.xml
├── SharePoint_RestAPI-01352B86-1861-EE11-BE6E-001DD8105346.json
├── SharePoint_RestAPI-01352B86-1861-EE11-BE6E-001DD8105346.json.data.xml
├── SyncuidmandatoryOffice-templateOutProcessingCheckl-E63625DB-8077-EE11-9AE5-001DD8105346.json
├── SyncuidmandatoryOffice-templateOutProcessingCheckl-E63625DB-8077-EE11-9AE5-001DD8105346.json.data.xml
├── templateOutProcessingChecklist-Generate-UID-ECF34AFB-0B8D-EE11-8179-001DD8105346.json
└── templateOutProcessingChecklist-Generate-UID-ECF34AFB-0B8D-EE11-8179-001DD8105346.json.data.xml
.gitignore
dcma_citdev.7d53a00d-09cc-eb21-8348-99a10042d965.json
dcma_dev.29e06d80-49ea-4b5a-8369-3be0329da8fc.json
dcma_prod.f9ad359e-3010-42a2-8e91-aa27b4428e44.json
dcma_test.3ddc5ce7-74d2-43d2-8324-17ba7baf8640.json
solutionPackage.zip
README.md
release-notes.html
```
# Deploy Solution Package

Deploying a solution package requires the scheduled Power Platform repository be cloned locally from the Git repository or the Solution Package be built locally on the host computer. Typically, the Power Platform repository is cloned from GitLab to be deployed in the upper environments.

### Example syntax
```powershell
.\deploy.ps1
```

Execute the deployment by running the **`.\Deploy.ps1`** script. A menu of available environments will be presented based on the `config.json`. 

Choose from one of the enviornment options by selecting a numbered configration:

```shell
CONFIGURED ENVIRONMENTS:

[ 1 ] DCMA_DEV
[ 2 ] DCMA_TEST
[ 3 ] DCMA_PROD
[ 4 ] DCMA_CITDEV
Select Environment Number (1,2,3,4): 
```

> Depending on your `config.json` file, you may see different options.

During the deployment, the script will automatically identify all the necessary files needed to deploy the Solution Package and Settings File.

## Git repository
After pulling the Power Platform and completing an unpack on the exported `.zip` file you must include the following `.gitignore` file within your GitLab Repository structure. Use this `.gitignore` file as baseline. This baseline structure ignores unecessary tracking on file types reflecting metadata changes that have no impact on source control.
```shell
## Ignore Folders
Entropy/
EditorState/
# Other/
PcfControlTemplates/
PcfConversions/
TableDefinitions/
Wadl/

## Ignore Files
*.gitignore
*_identity.json
*_BackgroundImageUri
*_DocumentUri.msapp
*.meta.xml
```
