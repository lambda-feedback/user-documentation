The Response Area Setup Panel component is called **ResponseAreaPanel** and it is located in the code under **modules/shared/components/ResponseArea**. It controls behaving of the whole Response Area Setup Panel and it wraps all Response Area Set Up Panel components.

## Response Area Setup Panel Components

### Input Type

- Control Type: ControlledSelect
- Values: hard-coded values defined in **EvaluationFunctionSupportedResponseType**.

### Evaluation Function

After the user select the Input Type, the Evaluation Function drop down list becomes populated by values linked to the selected Input Type (configured in the Evaluation Function page in the Admin context)

- Control Type: ControlledSelect
- Values:
    - query: TeacherGetFunctions
    - DB: EvaluationFunctions DB table (linked to Response Types through supportedResponseTypes column)

### Function Documentation

- Control Type: LabelledContent
- Value: TBA

### enable live preview

- Control Type: ControlledSwitch

### display input symbols

- Control Type: ControlledSwitch

### Pre Response Text

- Control Type: ControlledTextInput

### Response Area Answer

- Control Type: ResponseAreaAnswerInput

### Post Response Text

- Control Type: ControlledTextInput

### Response Area Preview

- Control Type: TestResponseArea

### Response Area Cases

- Control Type: ResponseAreaCases

## Submit

The Submit button click triggers onSave event - see the [Architecture](response_area-setup_panel_architecure.md) section for more information.