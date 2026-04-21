# User

Vrací informace o uživateli.

## Požadavek
```
GET /api/3/user
Content-Type: application/x-www-form-urlencoded
"Authorization: Bearer ACCESS_TOKEN"
```

## Odpověď

API ```3.43.0```
```200 OK```

```jsonc
{
  "UserUID": "1234/moje_id",
  "CampaignCategoryCode": "xxxxxxxxxxxxxxx_viz_níže_xxxxxxxxxxxxxxx",
  "Class": {
    "Id": "XL",
    "Abbrev": "X.A",
    "Name": "X.A" // nebo také prázdné!
  },
  "TeacherClasses": null,
  "FullName": "Příjmení Jméno, X.A",
  "SchoolOrganizationName": "název školy",
  "SchoolType": "BasicSchool", // Někdy null
  "UserType": "parents", // Možnosti "student", "parents", "teacher"
  "UserTypeText": "rodič",
  "StudyYear": 1,
  "EnabledModules": [ 
    {
      "Module": "Komens",
      "Rights": [
        "ShowReceivedMessages",
        "ShowSentMessages",
        "ShowNoticeBoardMessages",
        "SaveConcept",
        "ShowConcepts",
        "SendMessages",
        "ShowRatingDetails",
        "SendAttachments"
      ]
    },
    {
      "Module": "Absence",
      "Rights": [
        "ShowAbsence",
        "ShowAbsencePercentage"
      ]
    },
    {
      "Module": "Events",
      "Rights": [
        "ShowEvents"
      ]
    },
    {
      "Module": "Marks",
      "Rights": [
        "ShowFinalMarks",
        "ShowManners",
        "ShowMarks",
        "PredictMarks"
      ]
    },
    {
      "Module": "Timetable",
      "Rights": [
        "ShowTimetable"
      ]
    },
    {
      "Module": "Substitutions",
      "Rights": [
        "ShowSubstitutions"
      ]
    },
    {
      "Module": "Subjects",
      "Rights": [
        "ShowSubjects",
        "ShowSubjectThemes"
      ]
    },
    {
      "Module": "Homeworks",
      "Rights": [
        "ShowHomeworks"
      ]
    },
    {
      "Module": "Gdpr",
      "Rights": [
        "ShowOwnConsents",
        "ShowChildConsents",
        "ShowCommissioners"
      ]
    },
    {
      "Module": "Campaign",
      "Rights": [
        "ShowCampaign"
      ]
    },
    {
      "Module": "AccessSystem",
      "Rights": [
        "CanShowStudentPresentAtSchool"
      ]
    }
  ],
  "SettingModules": {
    "Komens": {
      "$type": "KomensModuleSettings",
      "UploadFolderVerified": true,
      "CurrentSchoolYearStartDate": "2025-08-20T00:00:00+02:00"
    },
    "Marking": {
      "$type": "MarksModuleSettings",
      "RequiredClassificationConfirmation": true,
      "ClassificationConfirmationClassesList": [],
      "ClassificationConfirmationNotification": true,
      "NumberOfDaysClassificationConfirmationNotifications": 14
    },
    "Homeworks": {
      "$type": "HomeworksModuleSettings",
      "UploadFolderVerified": true
    },
    "Common": {
      "$type": "CommonModuleSettings",
      "ActualSemester": {
        "SemesterId": "2",
        "From": "2026-01-04T00:00:00+01:00",
        "To": "2026-07-14T23:59:59+02:00"
      }
    },
    "Emergency": {
      "$type": "EmergencyModuleSettings",
      "FirestoreDbName": "production",
      "EmergencyServerUrl": "https://emergency.service.bakalari.cz"
    }
  },
  "FullUserName": "Příjmení Jméno",
  "Students": [
    {
      "FullName": "Příjmení Jméno, X.A",
      "Class": {
        "Id": "XL",
        "Abbrev": "X.A",
        "Name": "X. A" // nebo také prázdné!
      },
      "SchoolType": "BasicSchool",
      "StudyYear": 1
    }
  ]
}
```



### Význam ```CampaignCategoryCode```

Používá se u [informačního kanálu (campaign)](../campaign.md).

Po ```Base64``` dekódování dostaneme tuto strukturu:

```json
{
  "sid":"1234", //první část UserUID
  "ut":69,
  "sy":1        //study year
}
```

Study year se může na mobilu a na webu lišit, [viz #23](https://github.com/bakalari-api/bakalari-api-v3/issues/23).


## Chyby

při starém / neplatném ACCESS TOKENU

```401 Unauthorized```
```{"Message":"Authorization has been denied for this request."}```

při POST

```405 Method Not Allowed```
```{"Message":"The requested resource does not support http method 'POST'."}```

(Je možné, že o velkých prázdninách nebude vracet pololetí a možná ani moduly…)
