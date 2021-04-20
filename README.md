# i18n Visualizer
A new way to humanly source i18n translations by comparing a reference language side-by-side with the target language.

## Project Vision
- Owner signs in with GitHub, to create a project.
- Owner provides source language files in JSON.
- App extracts key/value pairs and adds them to a source data set.
- Owner can link screenshots to show the text in context (ie. the button on a page)
- Translator signs in with GitHub.
- Translator selects a project to translate.
- App displays the source texts and text boxes for target text.
- Translator translates source text to target language.
- Translator submits the translation.
- Translator is rewarded 10 points for their effort
- Owner sees the translation with a confidence level of accuracy.
- Translator can approve existing translations for the key/value or add a new one they believe to be better.


## API

### Projects
- `POST /projects` creates a new project
- `GET /projects` returns all my projects
- `GET /projects/{id}` returns a specific project (that I own)
- `PATCH /projects/{id}` updates a specific project (that I own)
- `DELETE /projects/{id}` deletes a specific project (that I own)

### Translations
- `POST /projects/{id}/translations` creates a new translation for a specific project
- `GET /projects/{id}/translations` returns all translations for a specific project
- `GET /projects/{id}/translations/{id}` returns a specific translation for a specific project
- `DELETE /projects/{id}/translations/{id}` deletes a specific translation (for a project that I own)


## Models

### Project
```javascript
{
  "id": ObjectId,
  "title": string,
  "description": string,
  "ownerId": string,
  "isActive": boolean,
  "sourceLanguage": string,
  "targetLanguages": [string],
  "sourceFiles": [Source] // TODO: Figure out how to store the file content better
}
```

### Translation
```javascript
{
  "id": ObjectId,
  "projectId": ObjectId,
  "userId": ObjectId,
  "targetLanguage": string,
  "translationValues": [Target] // TODO: Figure out how to handle translation values
}
```

### Source
```javascript
{
  "key": string,
  "value": string,
  "imageURL": string | undefined
}
```

### Target
```javascript
{
  "key": string,
  "originalText": string,
  "translatedText": string,
}
```
