### Template literals or String interpolation

You must already know what is template literals and how it works
    `${variable}`

    const student = {
      name: 'Richard Kalehoff',
      guardian: 'Mr. Kalehoff'
    };

    const teacher = {
      name: 'Mrs. Wilson',
      room: 'N231'
    }

    // without string interpolation
    let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';

    // with string interpolation
    let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;

    // multiline strings need new line chars without string interpolation
    let note = teacher.name + ',\n\n' +
      'Please excuse ' + student.name + '.\n' +
      'He is recovering from the flu.\n\n' +
      'Thank you,\n' +
      student.guardian;

    // string interpolation - no need of new line characters
    let note = 'teacher.name
      Please excuse ${student.name}
      'He is recovering from the flu
      Thank you,
      ${student.guardian}';

**TIP**: Embedded expressions inside template literals can do more than just reference variables. You can perform operations, call functions and use loops inside embedded expressions!
