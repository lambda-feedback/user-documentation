# Adding a new Response Area to Lambda Feedback

NameResponse represents the name of your response area (e.g. GraphResponse or ExpressionResponse). You may encounter various compilation errors while making steps along the way, however this is to be expected until all of the necessary file modifications have been made.

## `client-web`

### Files to add

If making a new response area, you will need to make some new files, or if you have the component already you may need to tweak it to work properly with the rest of the front end.

You will want to make a new folder titled _Name_ in the folder `client-web/components/ResponseArea/types`, where _Name_ is the name of your response area, e.g. _Graph_. You will want to start with this as this will inform you on which fields you need for your Response Area.

**Within `components/ResponseArea/types/`**

| Filepath                        | Required changes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| :------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| _<Name\>/index.ts_              | New file to export your _Name_ component.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| _<Name\>/<Name\>.schema.ts_     | New file with a zod parsing schema, you may be able to copy this from another type unless you need custom formats.                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| _<Name\>/<Name\>.module.css_    | New file which you may be able to copy and rename from another existing response area unless there are any specific css properties you would like to use.                                                                                                                                                                                                                                                                                                                                                                                                     |
| _<Name\>/<Name\>.component.tsx_ | New file where you will actually create and export your _Name_ component, the only required property it needs to take in as a property is a `handleChange` function which will be used to handle the submission of responses. Whatever you pass into `handleChange` is ultimately what will be passed as the _response_ field to the evaluation function, so if you have extra parameters that the student will input that the evaluation function requires you will need to pass them all in together as a dictionary object to the `handleChange` function. |
| _index.ts_                      | Just add a line to export everything from the new folder.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

**Within `modules/shared/components/ResponseArea/Input/`**

| Filepath                     | Required changes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :--------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _<Name\>Input.component.tsx_ | Optional component, this is where teachers would input properties required to create the response area, if you only require fields that the student can input to generate the response area then you can skip this step and use your _<Name\>.component.ts_ for the teachers to input as well. Otherwise you will want to set this up so that teachers can input any fields that you will need to create the Response Area for the student, preferably with default values. The only required property is the onChange function which will be used to save the teacher inputs. |
| _index.ts_                   | If you have decided to create the above Input component then you will need to export it here.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

### Files to modify

Most of these changes will involve adding your new response area to various switch statements or types, and passing all of the relevant fields that your response area needs to function.

It may be helpful to look at the relevant _Graph_ or _MultipleChoice_ versions of the response areas in each of these files as they have custom properties so you can see an example of the required foramts.

**Within `components/ResponseArea/`**

| Filepath                            | Required changes                                                                                                                                                                                                                                                                                                                                                  |
| :---------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _ResponseArea.component.tsx_        | Add a `StudentNameResponseArea` case to the ResponseArea switch statement returning your _<Name\>_ component, passing in the values you need as `field={area.field}` but excluding the `answer` field, in addition to passing in the `key`, `previousAnswer`, `handleChange` and `handleSubmit` properties the same way as is shown for the other response areas. |
| _TeacherResponseArea.component.tsx_ | Same as above but with `TeacherNameResponseArea` instead, and additionally including your answer field                                                                                                                                                                                                                                                            |

**Within `modules/shared/components/ResponseArea`**

| Filepath                                | Required changes                                                                                                                                                                                                                                                                                                                            |
| :-------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| _ResponseAreaAnswerInput.component.tsx_ | Add a case to the large switch statement for EvaluationFunctionSupportedResponseType.NAME, returning your _\<NameInput\>_ component if you decided to make one, or else returning your _<Name\>_ component instead. You may need to use your _responseAreaAnswerInputToNameData_ function defined above to extract the required properties. |
| _ResponseAreaInput.component.tsx_       | Similar setup to the above file change, except always returning your <Name\> component.                                                                                                                                                                                                                                                     |

**Within `modules/shared`**

| Filepath                                          | Required changes                                                                                                                                                                                                                      |
| :------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| _utils/response-area.utils.ts_                    | (Optional) If you have defined custom properties for your Response Area which means that you have more than one field, you may need to define a _responseAreaAnswerInputToNameData_ function to extract all the necessary properties. |
| _utils/shared-question-form.utils.ts_             | Similar to above but instead of returning a component, return an object called nameResponseInput with fields for each of your required properties.                                                                                    |
| _schemas/question-form.schema.ts_                 | (Optional) If you have custom properties, you will want to add to the _responseAreaAnswerInputSchema_ a z.object with all of your required fields, otherwise you can skip this step.                                                  |
| _hooks/useQuestionForm.defaults.ts_               | Add cases to switch statements for _TeacherNameResponseArea_ returning in the required format.                                                                                                                                        |
| _modules/teacher/utils/question-preview.utils.ts_ | Add cases to switch statements for respective _Name_ related cases.                                                                                                                                                                   |
| _types/responseArea.ts_                           |

You will need to export an interface _NameResponse_ in a similar format to the other response areas with your desired gradeFunction as the value of that field, you may want to use an existing one or create a new one. You will also need to add _NameResponse_ to the _ResponseArea_ type. |

**Within `api/documents/fragments/`**

| Filepath                                              | Required changes                                                                                                                                                                                                      |
| :---------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _response-area-type.fragment.graphql_                 | You will need to add _StudentNameResponseArea_ with all the types except for the saved answer field that you have decided above, copying the format of the other response areas by including \_\_typename as a field. |
| _teacher/teacher-response-area-type.fragment.graphql_ | Same as above but with _TeacherNameResponseArea_ and including the correct answer input by the teacher.                                                                                                               |

After making the necessary modifications to the API, you will need to autogenerate the _graphql.ts_ and _graphql-sdk.ts_ files again. This can be done by running `client-backend` locally:

```bash
docker compose build
docker compose up
```

and then running

```bash
yarn codegen
```

from client-web, you may want to stop the back-end running again before making the following back-end changes.

## `client-backend`

### Prisma

You will need to modify the prisma schema at _client-backend/prisma/schema.prisma_, if you are looking to modify an existing response area then you can simply add the required types to the appropriate response definition (e.g. ExpressionResponse), ideally setting a default value so that existing records for that response type in the database do not lack this field.
If adding a new response area, then you will need to create a new model structured as follows, with the fields as shown that are currently stored in all response types, plus the fields required for your response area component.

```prisma
model NameResponse {
    id             String       @id @default(uuid()) @db.Uuid
    createdAt      DateTime     @default(now())
    updatedAt      DateTime     @updatedAt
    deletedAt      DateTime?
    responseAreaId String       @unique @db.Uuid
    ResponseArea   ResponseArea @relation(fields: [responseAreaId], references: [id], onDelete: Cascade)
}
```

You will then also need to this new model to the `ResponseArea` model as the following field:

```prisma
NameResponse NameResponse?
```

After you have made these prisma changes, you will need to run the following in order to apply the prisma migrations to the database

```bash
npx prisma migrate dev
npx prisma generate
```

You will also need to run

```bash
docker compose build
```

before running the back-end again.

### Source Folder

Similar to the front end changes, it may be helpful to look at the _MultipleChoice_ or _Graph_ areas in each file to see which format to follow.

**Within `src/`**

| Filepath                                                | Required changes                                                                                                                                                           |
| :------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _response-area/teacher-response-area.union.ts_          | Export class _TeacherNameResponseArea_ with all necessary fields and add it to relevant types and switch cases.                                                            |
| _response-area/teacher-response-area.service.ts_        | Add _NameResponse_ as required across the file wherever _GraphResponse_ or _graphResponseInput_ has been placed.                                                           |
| _response-area/response-area.service.ts_                | Add _NameResponse_ to necessary types and add if statement at the bottom extracting properties from record.                                                                |
| _response-area/response-area.union.ts_                  | Export class _StudentNameResponseArea_ extending the _TeacherNameResponseArea_ omitting the teachers input answer field and add it to the relevant types and switch cases. |
| _response-area/inputs/teacher-create-response.input.ts_ | Make new class _NameResponseInput_ with all the required fields and add it to the _TeacherCreateResponseInput_ class.                                                      |
| _submission/submission.service.ts_                      | Add an if statement to _getAnswer_ to handle the _NameResponse_ case returning the answer field.                                                                           |
| _question/schemas/response-area.schema.ts_              | Add a zod schema for _NameResponseSchema_ with all required fields, add it into the _ResponseSchema_ and export _INameResponse_ similar to the other response areas.       |
| _question/entities/response-area.entity.ts_             | Add a _Name_ class and add it to relevant types and switch cases.                                                                                                          |

## Final Steps

Run the front and back end and test everything is working, hopefully compilation errors will show you where you need to tweak files in order to match the required formats, this document should include all the files that need modification for response area integration so if in doubt, look at the relevant file and compare what you have added to the existing response area implementations.
