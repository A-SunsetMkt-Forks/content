---
title: DOMMatrixReadOnly
slug: Web/API/DOMMatrixReadOnly
page-type: web-api-interface
browser-compat: api.DOMMatrixReadOnly
---

{{APIRef("Geometry Interfaces")}}{{AvailableInWorkers}}

The **`DOMMatrixReadOnly`** interface represents a read-only 4×4 matrix, suitable for 2D and 3D operations. The {{domxref("DOMMatrix")}} interface — which is based upon `DOMMatrixReadOnly`—adds [mutability](https://en.wikipedia.org/wiki/Immutable_object), allowing you to alter the matrix after creating it.

This interface should be available inside [web workers](/en-US/docs/Web/API/Web_Workers_API), though some implementations doesn't allow it yet.

## Constructor

- {{domxref("DOMMatrixReadOnly.DOMMatrixReadOnly", "DOMMatrixReadOnly()")}}
  - : Creates a new `DOMMatrixReadOnly` object.

## Instance properties

_This interface doesn't inherit any properties._

- {{domxref("DOMMatrixReadOnly.is2D")}} {{ReadOnlyInline}}
  - : A Boolean flag whose value is `true` if the matrix was initialized as a 2D matrix. If `false`, the matrix is 3D.
- {{domxref("DOMMatrixReadOnly.isIdentity")}} {{ReadOnlyInline}}
  - : A Boolean whose value is `true` if the matrix is an [identity matrix](https://en.wikipedia.org/wiki/Identity_matrix).
- `m11`, `m12`, `m13`, `m14`, `m21`, `m22`, `m23`, `m24`, `m31`, `m32`, `m33`, `m34`, `m41`, `m42`, `m43`, `m44`
  - : Double-precision floating-point values representing each component of a 4×4 matrix, where `m11` through `m14` are the first column, `m21` through `m24` are the second column, and so forth.
- `a`, `b`, `c`, `d`, `e`, `f`
  - : Double-precision floating-point values representing the components of a 4×4 matrix which are required in order to perform 2D rotations and translations. These are aliases for specific components of a 4×4 matrix, as shown below.

    | 2D  | 3D equivalent |
    | --- | ------------- |
    | `a` | `m11`         |
    | `b` | `m12`         |
    | `c` | `m21`         |
    | `d` | `m22`         |
    | `e` | `m41`         |
    | `f` | `m42`         |

## Instance methods

_This interface doesn't inherit any methods. None of the following methods alter the original matrix._

- {{domxref("DOMMatrixReadOnly.flipX()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by flipping the source matrix around its X-axis. This is equivalent to multiplying the matrix by `DOMMatrix(-1, 0, 0, 1, 0, 0)`. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.flipY()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by flipping the source matrix around its Y-axis. This is equivalent to multiplying the matrix by `DOMMatrix(1, 0, 0, -1, 0, 0)`. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.inverse()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by inverting the source matrix. The original matrix is not altered.
- {{domxref("DOMMatrixReadOnly.multiply()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by computing the dot product of the source matrix and the specified matrix. The original matrix is not
- {{domxref("DOMMatrixReadOnly.rotateAxisAngle()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by rotating the source matrix by the given angle around the specified vector. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.rotate()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by rotating the source matrix around each of its axes by the specified number of degrees. The original matrix is not altered.
- {{domxref("DOMMatrixReadOnly.rotateFromVector()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by rotating the source matrix by the angle between the specified vector and `(1, 0)`. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.scale()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by scaling the source matrix by the amount specified for each axis, centered on the given origin. By default, the X and Z axes are scaled by `1` and the Y axis has no default scaling value. The default origin is `(0, 0, 0)`. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.scale3d()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by scaling the source 3D matrix by the given factor along all its axes, centered on the specified origin point. The default origin is `(0, 0, 0)`. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.scaleNonUniform()")}} {{deprecated_inline}}
  - : Returns a new {{domxref("DOMMatrix")}} created by applying the specified scaling on the X, Y, and Z axes, centered at the given origin. By default, the Y and Z axes' scaling factors are both `1`, but the scaling factor for X must be specified. The default origin is `(0, 0, 0)`. The original matrix is not changed.
- {{domxref("DOMMatrixReadOnly.skewX()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by applying the specified skew transformation to the source matrix along its X-axis. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.skewY()")}}
  - : Returns a new {{domxref("DOMMatrix")}} created by applying the specified skew transformation to the source matrix along its Y-axis. The original matrix is not modified.
- {{domxref("DOMMatrixReadOnly.toFloat32Array()")}}
  - : Returns a new {{jsxref("Float32Array")}} of single-precision floating-point numbers, containing all 16 elements which comprise the matrix.
- {{domxref("DOMMatrixReadOnly.toFloat64Array()")}}
  - : Returns a new {{jsxref("Float64Array")}} of double-precision floating-point numbers, containing all 16 elements which comprise the matrix.
- {{domxref("DOMMatrixReadOnly.toJSON()")}}
  - : Returns a JSON representation of the `DOMMatrixReadOnly` object.
- {{domxref("DOMMatrixReadOnly.toString()")}}
  - : Creates and returns a string representation of the matrix in CSS matrix syntax, using the appropriate CSS matrix notation.
- {{domxref("DOMMatrixReadOnly.transformPoint()")}}
  - : Transforms the specified point using the matrix, returning a new {{domxref("DOMPoint")}} object containing the transformed point. Neither the matrix nor the original point are altered.
- {{domxref("DOMMatrixReadOnly.translate()")}}
  - : Returns a new {{domxref("DOMMatrix")}} containing a matrix calculated by translating the source matrix using the specified vector. By default, the vector is `(0, 0, 0)`. The original matrix is not changed.

## Static methods

- {{domxref("DOMMatrixReadOnly.fromFloat32Array_static", "fromFloat32Array()")}}
  - : Creates a new mutable `DOMMatrix` object given an array of single-precision (32-bit) floating-point values. If the array has six values, the result is a 2D matrix; if the array has 16 values, the result is a 3D matrix. Otherwise, a {{jsxref("TypeError")}} exception is thrown.
- {{domxref("DOMMatrixReadOnly.fromFloat64Array_static", "fromFloat64Array()")}}
  - : Creates a new mutable `DOMMatrix` object given an array of double-precision (64-bit) floating-point values. If the array has six values, the result is a 2D matrix; if the array has 16 values, the result is a 3D matrix. Otherwise, a {{jsxref("TypeError")}} exception is thrown.
- {{domxref("DOMMatrixReadOnly.fromMatrix_static", "fromMatrix()")}}
  - : Creates a new mutable `DOMMatrix` object given an existing matrix or an object which provides the values for its properties. If no matrix is specified, the matrix is initialized with every element set to `0` _except_ the bottom-right corner and the element immediately above and to its left: `m33` and `m34`. These have the default value of `1`.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- The mutable matrix type, {{domxref("DOMMatrix")}}, which is based on this one.
- The CSS {{cssxref("transform-function/matrix", "matrix()")}} and {{cssxref("transform-function/matrix3d", "matrix3d()")}} functional notation that can be generated from this interface to be used in a CSS {{cssxref("transform")}}.
