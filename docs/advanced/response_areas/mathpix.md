# Using MathPix for OCR and Mathematical Expressions

MathPix is a service for converting images and stroke data into a variety of formats for symbolic computation, as well as LaTeX. Currently, `client-backend` supports getting LaTeX equations from both stroke and image data.

In Lambda Feedback, we use MathPix to get a student's response from the handwriting and photo scanning modes of Expression Response Area. It is very simple to implement MathPix into a new response area if you need to convert images into mathematical equations.

## Integrating MathPix into your Response Area

The MathPix service in the backend is made available via GraphQL, using `useGetEquationFromStrokes.ts` and `useGetEquationFromImage.ts` hooks, which handle creating the GraphQL mutations `getEquationFromStrokes` and `getEquationFromImage` found in _api/documents/mutations_

`client-backend` caches the session IDs and app tokens automatically for each user according to their Imperial ID, and will automatically refresh once the tokens have expired.

### Stroke Data

In the response area component, initialise the hook

```typescript
const { postEquationStrokes, strokeEquation } = useGetEquationFromStrokes();
```

`postEquationStrokes` is called to get the latex equation from the backend, which is read from `strokeEquation`.

`postEquationStrokes` has the following call signature:

```typescript
function postEquationStrokes(x: number[][], y: number[][]): void;
```

Where `x` and `y` represent the x and y coordinates respectively, organised as a list of lists. The inner list represents all the coordinates of a single stroke, and the outer list is a collection of strokes.

Once the mutation has been made, `strokeEquation` will return the result with the following structure:

```typescript
interface MathpixResponse {
  latex?: string | null;
  confidence?: number | null;
  error?: string | null;
}
```

### Image

In the response area component, initialise the hook

```typescript
const { postEquationImage, imageEquation } = useGetEquationFromImage();
```

`postEquationImage()` has the following call signature:

```typescript
function postEquationImage(dataUrl: string): void;
```

Where `dataUrl` is the string representation of the image to evaluate.

!!! note
    GraphQL has a maximum payload size of 5 megabytes.
    You need to ensure the size of the `dataUrl` is less than this limit.

Similar to `strokeEquation`, `imageEquation` will have the following structure:

```typescript
interface MathpixResponse {
  latex?: string | null;
  confidence?: number | null;
  error?: string | null;
}
```
