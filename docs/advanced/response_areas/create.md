# Create a New Response Area

The
[`response-area-template`](https://github.com/lambda-feedback/response-area-template)
repository provides a pre-configured base for developing a new response
area. The template includes the [sandbox](sandbox.md) development tool which you
can use to view and test your response area.

## Prerequisites

You should be familiar with [Git](https://git-scm.com/),
[TypeScript](https://www.typescriptlang.org) and [React](https://react.dev).

## Implement your Response Area

1. [Create a new repository](https://github.com/new?template_name=response-area-template&template_owner=lambda-feedback)
   based on the template and clone it to your development machine.

1. Start the sandbox:
    ```
    $ ./start_sandbox
    ```

1. Implement your response area by editing the following files:

    - `components/Input.component.tsx`

        This React component should enable a student to enter their response.

    - `components/Wizard.component.tsx`

        This React component should allow a teacher to configure the response
        area.

1. Commit and push your changes to your repository on GitHub.
