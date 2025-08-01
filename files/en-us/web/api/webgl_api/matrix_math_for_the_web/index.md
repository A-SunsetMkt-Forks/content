---
title: Matrix math for the web
slug: Web/API/WebGL_API/Matrix_math_for_the_web
page-type: guide
---

{{DefaultAPISidebar("WebGL")}}

Matrices can be used to represent transformations of objects in space, and are used for performing many key types of computation when constructing images and visualizing data on the Web. This article explores how to create matrices and how to use them with [CSS transforms](/en-US/docs/Web/CSS/CSS_transforms/Using_CSS_transforms) and the `matrix3d` transform type.

While this article uses [CSS](/en-US/docs/Web/CSS) to simplify explanations, matrices are a core concept used by many different technologies including [WebGL](/en-US/docs/Web/API/WebGL_API), the [WebXR](/en-US/docs/Web/API/WebXR_Device_API) (VR and AR) API, and [GLSL shaders](/en-US/docs/Games/Techniques/3D_on_the_web/GLSL_Shaders).

## Transformation matrices

There are many types of matrices, but the ones we are interested in are the 3D transformation matrices. These matrices consist of a set of 16 values arranged in a 4×4 grid. In [JavaScript](/en-US/docs/Web/JavaScript), it is easy to represent a matrix as an array.

Let's begin by considering the **identity matrix**. This is a special transformation matrix which functions much like the number 1 does in scalar multiplication; just like n \* 1 = n, multiplying any matrix by the identity matrix gives a resulting matrix whose values match the original matrix.

The identity matrix looks like this in JavaScript:

```js
// prettier-ignore
const identityMatrix = [
  1, 0, 0, 0,
  0, 1, 0, 0,
  0, 0, 1, 0,
  0, 0, 0, 1,
];
```

What does multiplying by the identity matrix look like? The easiest example is to multiply a single point by the identity matrix. Since a 3D point only needs three values (`x`, `y`, and `z`), and the transformation matrix is a 4×4 value matrix, we need to add a fourth dimension to the point. By convention, this dimension is called the **perspective**, and is represented by the letter `w`. For a typical position, setting `w` to 1 will make the math work out.

After adding the `w` component to the point, notice how neatly the matrix and the point line up:

```js-nolint
[1, 0, 0, 0,
 0, 1, 0, 0,
 0, 0, 1, 0,
 0, 0, 0, 1];

[4, 3, 2, 1]; // Point at [x, y, z, w]
```

The `w` component has some additional uses that are out of scope for this article. Check out the [WebGL model view projection](/en-US/docs/Web/API/WebGL_API/WebGL_model_view_projection) article for a look into how it comes in handy.

### Multiplying a matrix and a point

In our example code we have defined a function to multiply a matrix and a point — `multiplyMatrixAndPoint()`:

```js live-sample___translation_matrix_ex live-sample___scale_matrix_ex live-sample___rotation_matrix_ex live-sample___matrix_composition_ex
// point • matrix
function multiplyMatrixAndPoint(matrix, point) {
  // Give a simple variable name to each part of the matrix, a column and row number
  const c0r0 = matrix[0],
    c1r0 = matrix[1],
    c2r0 = matrix[2],
    c3r0 = matrix[3];
  const c0r1 = matrix[4],
    c1r1 = matrix[5],
    c2r1 = matrix[6],
    c3r1 = matrix[7];
  const c0r2 = matrix[8],
    c1r2 = matrix[9],
    c2r2 = matrix[10],
    c3r2 = matrix[11];
  const c0r3 = matrix[12],
    c1r3 = matrix[13],
    c2r3 = matrix[14],
    c3r3 = matrix[15];

  // Now set some simple names for the point
  const x = point[0];
  const y = point[1];
  const z = point[2];
  const w = point[3];

  // Multiply the point against each part of the 1st column, then add together
  const resultX = x * c0r0 + y * c0r1 + z * c0r2 + w * c0r3;

  // Multiply the point against each part of the 2nd column, then add together
  const resultY = x * c1r0 + y * c1r1 + z * c1r2 + w * c1r3;

  // Multiply the point against each part of the 3rd column, then add together
  const resultZ = x * c2r0 + y * c2r1 + z * c2r2 + w * c2r3;

  // Multiply the point against each part of the 4th column, then add together
  const resultW = x * c3r0 + y * c3r1 + z * c3r2 + w * c3r3;

  return [resultX, resultY, resultZ, resultW];
}
```

> [!NOTE]
> Our examples on this page use row vectors to represent points and right-multiplication to apply transformation matrices. That is, the above does `point * matrix` where `point` is a 4x1 row vector. If you want to use column vectors and left-multiplication, you need to adjust the multiplication function accordingly, and transpose each matrix introduced below.
>
> For example, the [`translationMatrix`](#translation_matrix) introduced below originally looks like:
>
> ```js-nolint
> [1, 0, 0, 0,
>  0, 1, 0, 0,
>  0, 0, 1, 0,
>  x, y, z, 1]
> ```
>
> After transposition, it would look like:
>
> ```js-nolint
> [1, 0, 0, x,
>  0, 1, 0, y,
>  0, 0, 1, z,
>  0, 0, 0, 1]
> ```

Now using the function above we can multiply a point by the matrix. Using the identity matrix it should return a point identical to the original, since a point (or any other matrix) multiplied by the identity matrix is always equal to itself:

```js
// sets identityResult to [4,3,2,1]
const identityResult = multiplyMatrixAndPoint(identityMatrix, [4, 3, 2, 1]);
```

Returning the same point is not very useful, but there are other types of matrices that can perform helpful operations on points. The next sections will demonstrate some of these matrices.

### Multiplying two matrices

In addition to multiplying a matrix and a point together, you can also multiply two matrices together. The function from above can be re-used to help out in this process:

```js live-sample___translation_matrix_ex live-sample___scale_matrix_ex live-sample___rotation_matrix_ex live-sample___matrix_composition_ex
// matrixB • matrixA
function multiplyMatrices(matrixA, matrixB) {
  // Slice the second matrix up into rows
  const row0 = [matrixB[0], matrixB[1], matrixB[2], matrixB[3]];
  const row1 = [matrixB[4], matrixB[5], matrixB[6], matrixB[7]];
  const row2 = [matrixB[8], matrixB[9], matrixB[10], matrixB[11]];
  const row3 = [matrixB[12], matrixB[13], matrixB[14], matrixB[15]];

  // Multiply each row by matrixA
  const result0 = multiplyMatrixAndPoint(matrixA, row0);
  const result1 = multiplyMatrixAndPoint(matrixA, row1);
  const result2 = multiplyMatrixAndPoint(matrixA, row2);
  const result3 = multiplyMatrixAndPoint(matrixA, row3);

  // Turn the result rows back into a single matrix
  // prettier-ignore
  return [
    result0[0], result0[1], result0[2], result0[3],
    result1[0], result1[1], result1[2], result1[3],
    result2[0], result2[1], result2[2], result2[3],
    result3[0], result3[1], result3[2], result3[3],
  ];
}

function multiplyArrayOfMatrices(matrices) {
  if (matrices.length === 1) {
    return matrices[0];
  }
  return matrices.reduce((result, matrix) => multiplyMatrices(result, matrix));
}
```

Let's look at this function in action:

```js
// prettier-ignore
const someMatrix = [
  4, 0, 0, 0,
  0, 3, 0, 0,
  0, 0, 5, 0,
  4, 8, 4, 1,
];

// prettier-ignore
const identityMatrix = [
  1, 0, 0, 0,
  0, 1, 0, 0,
  0, 0, 1, 0,
  0, 0, 0, 1,
];

// Returns a new array equivalent to someMatrix
const someMatrixResult = multiplyMatrices(identityMatrix, someMatrix);
```

> [!WARNING]
> These matrix functions are written for clarity of explanation, not for speed or memory management. These functions create a lot of new arrays, which can be particularly expensive for real-time operations due to garbage collection. In real production code it would be best to use optimized functions. [glMatrix](https://glmatrix.net/) is an example of a library that has a focus on speed and performance. The focus in the glMatrix library is to have target arrays that are allocated before the update loop.

## Translation matrix

A **translation matrix** is based upon the identity matrix, and is used in 3D graphics to move a point or object in one or more of the three directions (`x`, `y`, and/or `z`). The easiest way to think of a translation is like picking up a coffee cup. The coffee cup must be kept upright and oriented the same way so that no coffee is spilled. It can move up in the air off the table and around the air in space.

You can't actually drink the coffee using only a translation matrix, because to drink it, you have to be able to tilt or rotate the cup to pour the coffee into your mouth. We'll look at the type of matrix (cleverly called a **[rotation matrix](#rotation_matrix)**) you use to do this later.

```js live-sample___translation_matrix_ex live-sample___matrix_composition_ex
function translate(x, y, z) {
  // prettier-ignore
  return [
    1, 0, 0, 0,
    0, 1, 0, 0,
    0, 0, 1, 0,
    x, y, z, 1,
  ];
}
```

Place the distances along the three axes in the corresponding positions in the translation matrix, then multiply it by the point or matrix you need to move through 3D space.

## Manipulating the DOM with a matrix

A really easy way to start using a matrix is to use the CSS {{cssxref("transform-function/matrix3d","matrix3d()")}} {{cssxref("transform")}}. First we'll set up a simple {{htmlelement("div")}} with some content. The style is not shown, but it's set to a fixed width and height and is centered on the page. The `<div>` has a transition set for the transform so that matrix is animated in making it easy to see what is being done.

```html live-sample___translation_matrix_ex live-sample___scale_matrix_ex live-sample___rotation_matrix_ex live-sample___matrix_composition_ex
<div class="transformable ghost">
  <h2>Move me with a matrix</h2>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
    quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
    consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
    cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
    non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
</div>

<div id="move-me" class="transformable">
  <h2>Move me with a matrix</h2>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
    quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
    consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
    cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
    non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
</div>
```

```css hidden live-sample___translation_matrix_ex live-sample___scale_matrix_ex live-sample___rotation_matrix_ex live-sample___matrix_composition_ex
.transformable {
  width: 200px;
  height: 200px;
  overflow-y: scroll;
  background: #4cc;
  padding: 10px;
  border: 2px solid #333;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -100px;
  margin-top: -100px;
  transition: transform 500ms;
}
.transformable h2 {
  margin-top: 0;
}
.ghost {
  opacity: 0.1;
  pointer-events: none;
}
```

Finally, for each example, we will generate a 4×4 matrix, then update the `<div>`'s style to have a transform applied to it, set to a `matrix3d`. Bear in mind that even though the matrix is made up of 4 rows and 4 columns, it collapses into a single line of 16 values. Matrices are always stored in one-dimensional lists in JavaScript.

```js live-sample___translation_matrix_ex live-sample___scale_matrix_ex live-sample___rotation_matrix_ex live-sample___matrix_composition_ex
// Create the matrix3d style property from a matrix array
function matrixArrayToCssMatrix(array) {
  return `matrix3d(${array.join(",")})`;
}

const moveMe = document.getElementById("move-me");

function setTransform(matrix) {
  moveMe.style.transform = matrixArrayToCssMatrix(matrix);
}
```

For one example, we use the `translate()` function from the [translation matrix](#translation_matrix) section above to move the `<div>` down 100 pixels and to the right 50 pixels. The `z` value is set to 0, so it doesn't move in the third dimension.

```js live-sample___translation_matrix_ex
const translationMatrix = translate(50, 100, 0);
setTransform(translationMatrix);
```

{{EmbedLiveSample("translation_matrix_ex", "", 350)}}

## Scale matrix

A **scale matrix** makes something larger or smaller in one or more of the three dimensions: width, height, and depth. In typical (cartesian) coordinates, this causes stretching or contracting of the object in the corresponding directions.

The amount of change to apply to each of the width, height, and depth is placed diagonally starting at the top-left corner and making their way down toward the bottom-right.

```js live-sample___scale_matrix_ex live-sample___matrix_composition_ex
function scale(x, y, z) {
  // prettier-ignore
  return [
    x, 0, 0, 0,
    0, y, 0, 0,
    0, 0, z, 0,
    0, 0, 0, 1,
  ];
}
```

```js live-sample___scale_matrix_ex
const scaleMatrix = scale(1.5, 0.7, 1);
setTransform(scaleMatrix);
```

{{EmbedLiveSample("scale_matrix_ex", "", 350)}}

## Rotation matrix

A **rotation matrix** is used to rotate a point or object. Rotation matrices look a little bit more complicated than scaling and transform matrices. They use trigonometric functions to perform the rotation. While this section won't break the steps down into exhaustive detail (check out [this article on Wolfram MathWorld](https://mathworld.wolfram.com/RotationMatrix.html) for that), take this example for illustration.

First, here's code that rotates a point around the origin without using matrices.

```js
// Manually rotating a point about the origin without matrices
const point = [10, 2];

// Calculate the distance from the origin
const distance = Math.sqrt(point[0] * point[0] + point[1] * point[1]);

// The equivalent of 60 degrees, in radians
const rotationInRadians = Math.PI / 3;

const transformedPoint = [
  Math.cos(rotationInRadians) * distance,
  Math.sin(rotationInRadians) * distance,
];
```

It is possible to encode these type of steps into a matrix, and do it for each of the `x`, `y`, and `z` dimensions. Here are a set of functions that return rotation matrices for rotating around each of the three axes. One big note is that there is no perspective applied, so it might not feel very 3D yet. The flatness is equivalent to when a camera zooms in really close onto an object in the distance — the sense of perspective disappears.

```js live-sample___rotation_matrix_ex live-sample___matrix_composition_ex
const sin = Math.sin;
const cos = Math.cos;

function rotateX(a) {
  // prettier-ignore
  return [
    1, 0, 0, 0,
    0, cos(a), -sin(a), 0,
    0, sin(a), cos(a), 0,
    0, 0, 0, 1,
  ];
}

function rotateY(a) {
  // prettier-ignore
  return [
    cos(a), 0, sin(a), 0,
    0, 1, 0, 0,
    -sin(a), 0, cos(a), 0,
    0, 0, 0, 1,
  ];
}

function rotateZ(a) {
  // prettier-ignore
  return [
    cos(a), -sin(a), 0, 0,
    sin(a), cos(a), 0, 0,
    0, 0, 1, 0,
    0, 0, 0, 1,
  ];
}
```

```js live-sample___rotation_matrix_ex
const rotateZMatrix = rotateZ(Math.PI * 0.3);
setTransform(rotateZMatrix);
```

{{EmbedLiveSample("rotation_matrix_ex", "", 350)}}

## Matrix composition

The real power of matrices comes from **matrix composition**. When matrices of a certain class are multiplied together they preserve the history of the transformations and are reversible. This means that if a translation, rotation, and scale matrix are all combined together, when the order of the matrices is reversed and re-applied, then the original points are returned.

The order that matrices are multiplied in matters. When multiplying numbers, a \* b = c, and b \* a = c are both true. For example 3 \* 4 = 12, and 4 \* 3 = 12. In math, these numbers would be described as **commutative**. Matrices are _not_ guaranteed to be the same if the order is switched, so matrices are **non-commutative**.

Another mind-bender is that matrix multiplication in WebGL and CSS needs to happen in the reverse order that the operations intuitively happen. For instance, to scale something down by 80%, move it down 200 pixels, and then rotate about the origin 90 degrees would look something like the following in pseudocode.

```plain
transformation = rotate * translate * scale
```

### Composing multiple transformations

The function that we will be using to compose our matrices is `multiplyArrayOfMatrices()`, which is part of the set of utility functions introduced near the top of this article. It takes an array of matrices and multiplies them together, returning the result. In WebGL shader code, this is built into the language and the `*` operator can be used.

```js live-sample___matrix_composition_ex
const transformMatrix = multiplyArrayOfMatrices([
  rotateZ(Math.PI * 0.5), // Step 3: rotate around 90 degrees
  translate(0, 200, 0), // Step 2: move down 200 pixels
  scale(0.8, 0.8, 0.8), // Step 1: scale down
]);

setTransform(transformMatrix);
```

{{EmbedLiveSample("matrix_composition_ex", "", 350)}}

Finally, a fun step to show how matrices work is to reverse the steps to bring the matrix back to the original identity matrix.

```js
const transformMatrix = multiplyArrayOfMatrices([
  scale(1.25, 1.25, 1.25), // Step 6: scale back up
  translate(0, -200, 0), // Step 5: move back up
  rotateZ(-Math.PI * 0.5), // Step 4: rotate back
  rotateZ(Math.PI * 0.5), // Step 3: rotate around 90 degrees
  translate(0, 200, 0), // Step 2: move down 200 pixels
  scale(0.8, 0.8, 0.8), // Step 1: scale down
]);
```

## Why matrices are important

Matrices are important because they comprise a small set of numbers that can describe a wide range of transformations in space. They can easily be shared around in programs. Different coordinate spaces can be described with matrices, and some matrix multiplication will move one set of data from one coordinate space to another coordinate space. Matrices effectively remember every part of the previous transforms that were used to generate them.

For uses in WebGL, the graphics card is particularly good at multiplying a large number of points in space by matrices. Different operations like positioning points, calculating lighting, and posing animated characters all rely on this fundamental tool.
