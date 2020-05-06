### Destructuring

Destructuring borrows inspiration from languages like Perl and Python by allowing you to specify the elements you want to extract from an array or object on the left side of an assignment.

    const point = [10, 25, -34];
    const [x, y, z] = point;
    const [a, , c] = point;
    console.log(x, y, z); // 10 25 -34
    console.log(a, c); // 10 -34


Destructuring objects and functions inside them

    const circle = {
      radius: 10,
      color: 'orange',
      getArea: function() {
        return Math.PI * this.radius * this.radius;
      },
      getCircumference: function() {
        return 2 * Math.PI * this.radius;
      }
    };

    let {radius, getArea, getCircumference} = circle;
    getArea();

what would be the output? many would guess 314.159 but it would be NaN actually

When you destructure the object and store the getArea() method into the getArea variable, it no longer has access to this in the circle object which results in an area that is NaN.