En la f谩brica de Papa No茅l 馃巺 se acerca el d铆a especial... y todav铆a tenemos un mont贸n de cosas por contar. 馃槄

Por suerte a Mark Zucktheelf 馃 se le ha ocurrido crear una funci贸n que permita agrupar un array, que puede ser de valores u objetos, a trav茅s de una funci贸n o de una propiedad.

Nos trae un mont贸n de ejemplos:

```js
groupBy([6.1, 4.2, 6.3], Math.floor) // { 6: [6.1, 6.3], 4: [4.2] }
groupBy(['one', 'two', 'three'], 'length') // { 3: ['one', 'two'], 5: ['three'] }
groupBy([{age: 23}, {age: 24}], 'age') // { 23: [{age: 23}], 24: [{age: 24}] }

groupBy(
  [1397639141184, 1363223700000],
  timestamp => new Date(timestamp).getFullYear()
)
// { 2013: [1363223700000], 2014: [1397639141184] }

groupBy([
  { title: 'JavaScript: The Good Parts', rating: 8 },
  { title: 'Aprendiendo Git', rating: 10 },
  { title: 'Clean Code', rating: 9 },
], 'rating')
// { 8: [{ title: 'JavaScript: The Good Parts', rating: 8 }],
//   9: [{ title: 'Clean Code', rating: 9 }],
//   10: [{ title: 'Aprendiendo Git', rating: 10 }] }
```

Como ves, la funci贸n groupBy recibe una colecci贸n (array) y una funci贸n o una propiedad, y devuelve un objeto con claves que son los valores de la funci贸n ejecutada pasando como argumento cada elemento o de la propiedad por cada elemento. Luego los valores son un array de los valores que tengan la misma llave.

La dificultad del reto est谩 m谩s en comprender la funci贸n que en la implementaci贸n. 隆Suerte!. <br ><br >

## **Soluci贸n**

```js
export default function groupBy(collection, it) {
  let RESULT = {};

  const EXECUTABLE = (param) => {
    switch (typeof it) {
      case "function":
        return it(param);

      case "string":
        return param[it];
    }
  };

  collection.forEach((elm) => {
    const AUX = EXECUTABLE(elm);

    if (!RESULT[AUX]) {
      RESULT[AUX] = [elm];
    } else {
      RESULT[AUX].push(elm);
    }
  });

  return RESULT;
}
```