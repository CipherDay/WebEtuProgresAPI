# WebEtu Progres API:

## Table of content:

<!-- TOC -->

- [WebEtu Progres API:](#webetu-progres-api)
  - [Table of content:](#table-of-content)
  - [1. Overview:](#1-overview)
  - [2. How the docs are structured:](#2-how-the-docs-are-structured)
  - [3.Endpoints:](#3endpoints)

<!-- TOC -->

## 1. Overview:

- ### Introduction:

This API documents are for the WebEtu progres app considering the lack of online information about the api I created
these docs from what I was able to reverse engineer form the android app so take those docs with grain of salt for
they are not official or complete.

- ### Base url:

All calls to the api are made through the following url: `https://progres.mesrs.dz/api/` or `https://api-webetu.mesrs.dz/api/` they interchangeable.

- ### Authentication:

Almost every call to the api require an `Authorization:<token>` header.

## 2. How the docs are structured:

Because the lack of the full picture the docs won't be structured like the usual api docs, All the endpoint are under
the base url except some that are nested, Unless is stated otherwise the endpoint is under the base url.

## 3.Endpoints:

- ### Auth:
- #### POST `/authentication/v1/`
- **Description:** Authenticate a user and return an access token.
- **Methode:** `POST`.
- **Content-Type:** `application/json`.
- ##### Request:
- Headers:

| Key            | Value              | Required |
| -------------- | ------------------ | -------- |
| `Content-Type` | `application/json` | `true`   |

- Body:

```json
{
  "password": "string",
  "username": "string"
}
```

- ##### Response:
- Success (200):

```json
{
  "expirationDate": "ISO 8601 time",
  "token": "string",
  "userId": 999999,
  "uuid": "ISO 8601 time",
  "idIndividu": 999999,
  "etablissementId": 9999999,
  "userName": "string"
}
```

- Forbidden (403):

`Mot de passe ou nom utilisateur incorrecte`

- ### Infos:
- #### GET `/infos/configuration`:
- **Description:** Get the current config.
- **Methode:** `GET`.
- **authorization:** `null`.
- ##### Response:
- Success (200):

```json
{
  "option1": false,
  "option2": false,
  "option3": true,
  "option4": true,
  "option5": true,
  "option6": true,
  "option7": true,
  "option8": true,
  "option9": true,
  "option10": true,
  "option11": true,
  "option12": true,
  "option13": true,
  "newsPageUrl": "string"
}
```

- #### GET `/infos/AnneeAcademiqueEncours`:
- **Description:** Get the current running academic year.
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
{
  "id": 99,
  "code": "string",
  "libelle": null
}
```

- Forbidden (403):

```ignore
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/dias`:
- **Description:** Get all available academic years for the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
    {
    "id": 9999999,
    "numeroInscription": "string",
    "anneeAcademiqueId": 99,
    "anneeAcademiqueCode": "string",
    "situationId": 99,
    "dossierEtudiantId": 9999999,
    "numeroMatricule": "string",
    "ouvertureOffreFormationId": 999999,
    "refCodeCycle": "string",
    "refLibelleCycle": "string",
    "refLibelleCycleAr": "string",
    "ofIdDomaine": 99999,
    "ofCodeDomaine": "string",
    "ofLlDomaine": "string",
    "ofLlDomaineArabe": "string",
    "ofIdFiliere": 99999,
    "ofCodeFiliere": "string",
    "ofLlFiliereArabe": "string",
    "ofLlFiliere": "string",
    "individuId": 999999,
    "nin": "string",
    "individuNomArabe": "string",
    "individuNomLatin": "string",
    "individuPrenomArabe": "string",
    "individuPrenomLatin": "string",
    "individuDateNaissance": "ISO 8601 time",
    "individuLieuNaissance": "string",
    "individuLieuNaissanceArabe": "string",
    "refEtablissementId": 999999,
    "refCodeEtablissement": "string",
    "llEtablissementArabe": "string",
    "llEtablissementLatin": "string",
    "moyenneBac": 99.99,
    "lastMoyenne": 99.99,
    "photo": "string",
    "cycleId": 99999,
    "cycleCode": "string",
    "cycleLibelleLongLt": "string",
    "niveauId": 99999,
    "niveauCode": "string",
    "niveauRang": 99999,
    "niveauLibelleLongLt": "string",
    "niveauLibelleLongAr": "string",
    "transportPaye": true,
    "fraisInscriptionPaye": true
    },
    { ... }
]
```

- Forbidden (403):

```ignore
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/anneeAcademique/{id}/dia`:
- **Description:** Get the specified academic year by [`id`](#GET-infosAnneeAcademiqueEncours) for the specified user [
  `uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |
| `id`      | number | The unique year ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
{
  "id": 9999999,
  "numeroInscription": "string",
  "anneeAcademiqueId": 99999,
  "anneeAcademiqueCode": "string",
  "situationId": 99,
  "dossierEtudiantId": 999999,
  "numeroMatricule": "string",
  "ouvertureOffreFormationId": 9999,
  "refCodeCycle": "string",
  "refLibelleCycle": "string",
  "refLibelleCycleAr": "string",
  "ofIdDomaine": 99999,
  "ofCodeDomaine": "string",
  "ofLlDomaine": "string",
  "ofLlDomaineArabe": "string",
  "ofIdFiliere": 99999,
  "ofCodeFiliere": "string",
  "ofLlFiliereArabe": "string",
  "ofLlFiliere": "string",
  "individuId": 99999999,
  "nin": "string",
  "individuNomArabe": "string",
  "individuNomLatin": "string",
  "individuPrenomArabe": "string",
  "individuPrenomLatin": "string",
  "individuDateNaissance": "ISO 8601 time",
  "individuLieuNaissance": "string",
  "individuLieuNaissanceArabe": "string",
  "refEtablissementId": 9999999,
  "refCodeEtablissement": "string",
  "llEtablissementArabe": "string",
  "llEtablissementLatin": "string",
  "moyenneBac": 99.99,
  "lastMoyenne": 99.99,
  "photo": "string",
  "cycleId": 99999,
  "cycleCode": "string",
  "cycleLibelleLongLt": "string",
  "niveauId": 99999,
  "niveauCode": "string",
  "niveauRang": 99999,
  "niveauLibelleLongLt": "string",
  "niveauLibelleLongAr": "string",
  "transportPaye": true,
  "fraisInscriptionPaye": true
}
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/notes`:
- **Description:** Get the BAC notes for the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
    {
    "note": 99.99,
    "refCodeMatiereLibelleFr": "string"
    },
    {
    "note": 99.99,
    "refCodeMatiereLibelleFr": "string"
    },
    { ... }
]
```

- Forbidden (403):

```ignore
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/individ`:
- **Description:** Get general information about the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
{
  "id": 99999999,
  "identifiant": "string",
  "dateNaissance": "ISO 8601 time",
  "nomArabe": "string",
  "nomLatin": "string",
  "prenomArabe": "string",
  "prenomLatin": "string",
  "lieuNaissance": "string",
  "lieuNaissanceArabe": "string",
  "photo": "string",
  "email": null,
  "idCarde": "string"
}
```

- Forbidden (403):

```ignore
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/demandesHebregement`:
- **Description:** Get housing information about the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
  {
    "id": 999999,
    "idDia": 9999999,
    "numeroInscription": "string",
    "idDossierEtudiant": 9999999,
    "numeroMatricule": "string",
    "idAnneeAcademique": 99999,
    "codeAnneeAcademique": "string",
    "idDou": 9999999,
    "llDou": "string",
    "llDouArabe": "string",
    "idResidence": null,
    "llResidance": "string",
    "llResidanceArabe": "string",
    "dateDemandeHeb": "ISO 8601 time",
    "approuveeHebDou": true,
    "approuveeHebDou1": true,
    "dateApprouveHebDou": null,
    "renouvellement": true,
    "llAffectation": "ISO 8601 time",
    "demandeRenouvellement": true,
    "dateDemandeRenouvellement": "ISO 8601 time",
    "idCycle": 99,
    "llCycle": "string",
    "llCycleArabe": "string",
    "codeCycle": "string",
    "idNiveau": 99999,
    "llNiveau": "string",
    "llNiveauArabe": "string",
    "codeNiveau": "string",
    "idEtablissement": 99999999,
    "llEtablissement": "string",
    "llEtablissementArabe": "string",
    "idDomaine": 9,
    "llDomaine": "string",
    "llDomaineArabe": "string",
    "hebergementPaye": true
  }
]
```

- Forbidden (403):

```ignore
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/dia/{id}/annuel/bilan`:
- **Description:** Get the performance in the specified academic year by [`id`](#GET-infosbacuuidanneeAcademiqueiddia)
  for the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |
| `id`      | number | The unique year ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
  {
    "id": 9999999,
    "type": 99999,
    "bilanUes": [],
    "typeDecisionLibelleFr": "string",
    "typeDecisionLibelleAr": "string",
    "moyenne": 99.99,
    "moyenneSn": 99.99,
    "credit": 99.99,
    "creditObtenu": 99.99,
    "creditAcquis": 99.99,
    "annuel": true,
    "niveauRang": 99999,
    "totalAquis": 99999,
    "effectif": 99999,
    "coefficient": 99.99
  }
]
```

- Forbidden (403):

```ignore
EMPTY BODY
```

- #### GET `/infos/bac/{uuid}/dia/{id}/periode/bilans`:
- **Description:** Get the performance of all the periods in the specified academic year by [
  `id`](#GET-infosbacuuidanneeAcademiqueiddia) for the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |
| `id`      | number | The unique year ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
    {
        "id": 99999999,
        "type": 99999,
        "periodeId": 99999,
        "periodeLibelleFr": "string",
        "periodeLibelleAr": "string",
        "bilanUes": [
            {
            "id": 99999999,
            "bilanSessionId": 99999999,
            "repartitionUeId": 99999999,
            "ueLibelleFr": "string",
            "ueCode": "string",
            "ueType": "string",
            "moyenne": 99.99,
            "coefficient": 99.99,
            "credit": 99.99,
            "creditObtenu": 99.99,
            "creditAcquis": 99.99,
            "ueNatureLcFr": "string",
            "ueNatureLcAr": "string",
            "ueNatureCode": "string",
            "bilanMcs": [
                {
                "id": 99999999,
                "bilanUeId": 99999999,
                "bilanSessionId": 99999999,
                "rattachementMcId": 99999999,
                "mcLibelleFr": "string",
                "mcLibelleAr": "string",
                "mcCode": "string",
                "coefficient": 99.99,
                "credit": 99.99,
                "creditObtenu": 99.99,
                "moyenneGenerale": 99.99
                }
            ],
            "ueNoteObtention": 99.99,
            "ueAcquis": false,
            "totalAquis": 99999,
            "effectif": 0
            },
            { ... }
        ],
        "moyenne": 99.99,
        "moyenneSn": 99.99,
        "credit": 99.99,
        "creditObtenu": 99.99,
        "creditAcquis": 99.99,
        "annuel": false,
        "cycleLibelleLongLt": "string",
        "niveauCode": "string",
        "niveauRang": 99999,
        "niveauLibelleLongLt": "string",
        "niveauLibelleLongAr": "string",
        "totalAquis": 99999,
        "effectif": 99999,
        "coefficient": 99.99
        },
        {
        "id": 99999999,
        "type": 99999,
        "periodeId": 99,
        "periodeLibelleFr": "string",
        "periodeLibelleAr": "string",
        "bilanUes": [
        { .... }
        ],
        "moyenne": 99.99,
        "moyenneSn": 99.99,
        "credit": 99.99,
        "creditObtenu": 99.99,
        "creditAcquis": 99.99,
        "annuel": false,
        "cycleLibelleLongLt": "string",
        "niveauCode": "string",
        "niveauRang": 99999,
        "niveauLibelleLongLt": "string",
        "niveauLibelleLongAr": "string",
        "totalAquis": 99999,
        "effectif": 99999,
        "coefficient": 99.99
    }
]
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/controleContinue/dia/{id}/notesCC`:
- **Description:** Get TD/TP notes about the specified academic year [
  `id`](#GET-infosbacuuidanneeAcademiqueiddia).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description                  | Required |
| --------- | ------ | ---------------------------- | -------- |
| `id`      | Number | The unique academic year ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
    {
    "id": 99999999,
    "note": 99.99,
    "absent": false,
    "observation": "",
    "llPeriode": "string",
    "llPeriodeAr": "string",
    "apCode": "string",
    "rattachementMcMcLibelleFr": "string",
    "rattachementMcMcLibelleAr": "string",
    "dateDebutDepotRecours": "ISO 8601 time",
    "dateLimiteDepotRecours": "ISO 8601 time",
    "autorisationDemandeRecours": false
    },
    { ... }
]
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/planningSession/dia/{id}/noteExamens`:
- **Description:** Get Exams notes about the specified academic year [`id`](#GET-infosbacuuidanneeAcademiqueiddia).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description                  | Required |
| --------- | ------ | ---------------------------- | -------- |
| `id`      | Number | The unique academic year ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
   {
       "id": 99999999,
       "rattachementMcId": 99999999,
       "ueCode": "string",
       "ueNatureLlFr": "string",
       "mcLibelleFr": "string",
       "mcLibelleAr": "string",
       "rattachementMcCoefficient": 99.99,
       "rattachementMcCredit": 99.99,
       "planningSessionId": 99999,
       "planningSessionIntitule": "string",
       "idPeriode": 99999,
       "noteExamen": 99.99,
       "dateDebutDepotRecours": "ISO 8601 time",
       "dateLimiteDepotRecours": "ISO 8601 time",
       "autorisationDemandeRecours": false
   },
   { ... }
]
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/Examens/{id}/niveau/{niveauId}/examens`:
- **Description:** Get Exams timetable of the specified level [`niveauId`](#GET-infosbacuuidanneeAcademiqueiddia) about
  the specified academic year [`id`](#GET-infosbacuuidanneeAcademiqueiddia).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter  | Type   | Description                    | Required |
| ---------- | ------ | ------------------------------ | -------- |
| `id`       | Number | The unique academic year ID.   | yes      |
| `niveauId` | Number | The unique number of the level | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
   {
       "anonymat": false,
       "dateExamen": "ISO 8601 time",
       "duree": 99999,
       "heureDebut": "ISO 8601 time",
       "heureFin": "ISO 8601 time",
       "id": 99999999,
       "libellePeriode": "string",
       "libellePeriodeAr": "string",
       "mcLibelleAr": "string",
       "mcLibelleFr": "string",
       "moyenneSession": 99.99,
       "noteGereParEnseignant": true,
       "planningCoefficientNoteEliminatoire": 99.99,
       "typeSession": "string",
       "typeSessionAr": "string"
   },
   { .... }
]
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/api/infos/niveau/{niveauId}/periodes`:
- **Description:** Get the periods of the specified level [`niveauId`](#GET-infosbacuuidanneeAcademiqueiddia).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter  | Type   | Description                    | Required |
| ---------- | ------ | ------------------------------ | -------- |
| `niveauId` | Number | The unique number of the level | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
  {
    "code": "string",
    "credit": 99999,
    "id": 99999,
    "libelleCourtAr": null,
    "libelleCourtLt": null,
    "libelleLongAr": "string",
    "libelleLongFrCycle": "string",
    "libelleLongFrNiveau": "string",
    "libelleLongLt": "string",
    "ncPeriodeCode": null,
    "ncPeriodeId": null,
    "ncPeriodeLibelle": null,
    "rang": 99999,
    "rangNiveau": 99999,
    "refCodePeriode": null,
    "refCodePeriodicite": null
  },
  {
    "code": "string",
    "credit": 99999,
    "id": 99999,
    "libelleCourtAr": null,
    "libelleCourtLt": null,
    "libelleLongAr": "string",
    "libelleLongFrCycle": "string",
    "libelleLongFrNiveau": "string",
    "libelleLongLt": "string",
    "ncPeriodeCode": null,
    "ncPeriodeId": null,
    "ncPeriodeLibelle": null,
    "rang": 99999,
    "rangNiveau": 99999,
    "refCodePeriode": null,
    "refCodePeriodicite": null
  }
]
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/dettes/{uuid}`:
- **Description:** Get debit information about the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```
TBD
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/demandeTransport/{uuid}`:
- **Description:** Get transportation information about the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
{
  "dateDemandeTransport": "ISO 8601 time",
  "id": 99999999,
  "transportPayed": true
}
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/dia/{id}/groups`:
- **Description:** Get group of the user in the specified academic year [`id`](#GET-infosbacuuidanneeAcademiqueiddia).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description                  | Required |
| --------- | ------ | ---------------------------- | -------- |
| `id`      | Number | The unique academic year ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```json
[
  {
    "dateAffectation": "ISO 8601 time",
    "groupePedagogiqueId": 99999999,
    "id": 99999999,
    "nomGroupePedagogique": "string",
    "periodeCode": "string",
    "periodeId": 99999,
    "periodeLibelleLongLt": "string"
  },
  {
    "dateAffectation": "ISO 8601 time",
    "groupePedagogiqueId": 99999999,
    "id": 99999999,
    "nomGroupePedagogique": "string",
    "nomSection": "string",
    "periodeCode": "string",
    "periodeId": 99999,
    "periodeLibelleLongLt": "string"
  }
]
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/image/{uuid}`:
- **Description:** Get card image of the specified user [`uuid`](#Auth).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter | Type   | Description         | Required |
| --------- | ------ | ------------------- | -------- |
| `uuid`    | String | The unique user ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```
A Base64 encoded image
```

- Forbidden (403):

```
EMPTY BODY
```

- #### GET `/infos/logoEtablissement/{refEtablissementId}`:
- **Description:** Get logo of the specified university [`refEtablissementId`](#GET-infosbacuuidanneeAcademiqueiddia).
- **Methode:** `GET`.
- **Authorization:** `token`.
- ##### Path parameters:

| Parameter            | Type   | Description               | Required |
| -------------------- | ------ | ------------------------- | -------- |
| `refEtablissementId` | Number | The unique university ID. | yes      |

- ##### Request:
- Headers:

| Key             | Value   | Required |
| --------------- | ------- | -------- |
| `Authorization` | `token` | `true`   |

- ##### Response:
- Success (200):

```
A Base64 encoded image
```

- Forbidden (403):

```
EMPTY BODY
```
