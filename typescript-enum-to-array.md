# Typescript enum to array

_Status: Published_
_Created: 2021-09-09 02:33:07_
_Tags: typescript, Typescript, javascript, ts_

<code>
// enum with string values
enum Lines {
    Line1 = 'text1',
    Line2 = 'text2',
    Line3 = 'text3'
}
// enum
enum State {
    Start,
    Running,
    Stop
}

function ToArray(lines: any) {
    return Object.keys(lines)
        .filter(l => typeof l === "string")
        .map(l => lines[l]);
}

const arr = ToArray(Lines);

console.log(ToArray(arr)); //  ["text1", "text2", "text3"]

const arr2 = ToArray(State);

console.log(ToArray(arr2)); // ["Start", "Running", "Stop", 0, 1, 2]  ??? 0, 1, 2 are no strings??? 
</code>