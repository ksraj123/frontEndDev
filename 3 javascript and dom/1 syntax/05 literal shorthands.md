### Object literal shorthand

You’ve probably written code where an object is being initialized using the same property names as the variable names being assigned to them.

    let type = 'quartz';
    let color = 'rose';
    let carat = 21.29;

    const gemstone = {
        type: type,
        color: color,
        carat: carat
    };

    console.log(gemstone);

In a stituation like this we can simple do -

    const gemstone = {type, color, carat};

and a function can also be added inside an object just by its name

    let gemstone = {
        type,
        color,
        carat,
        calculateWorth() { ... }
    };