# Template tags

They don't have to return strings!

    % node
    > function r(strings, oneExp) { return oneExp }
    undefined
    > r`nothing ${100}`
    100
    > r`nothing ${ { a: 1, b: { c: 3, d: 4 }}}`
    { a: 1, b: { c: 3, d: 4 } }
    > r`nothing ${ { a: 1 } } ${ { b: 2 }} , `
    { a: 1 }
    > function r(strings, oneExp) { return [oneExp, arguments[2] }
    ... function r(strings, oneExp) { return [oneExp, arguments[2]] }
    ... 
    > function r(strings, oneExp) { return [oneExp, arguments[2]] }
    undefined
    > r`nothing ${ { a: 1 } } ${ { b: 2 }} , `
    [ { a: 1 }, { b: 2 } ]
    > 
