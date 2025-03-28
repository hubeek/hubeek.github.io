# RxJs 

_Status: Published_
_Created: 2020-03-13 04:04:31_
_Tags: javascript_

useful site to exercise:
[Stephen Grider RxJs playground](https://out.stegrider.now.sh)

```
const { fromEvent } = Rx;
const { map, pluck } = RxOperators;

const input = document.createElement('input');
const container = document.querySelector('.container');
container.appendChild(input);

const observable = fromEvent(input, 'input')
.pipe(
	pluck('target','value'),
  map(value=>parseInt(value)),
  map(value => {
    if(isNaN(value)){
    	throw Error('The input must be a number.')
    }
    return value;
  })
);

observable.subscribe({
	next(value){
  	console.log('You inserted '+value);
  },
  error(err){
  	console.error('error : '+err.message);
  },
  complete(){},
});

observable;
```
result:
```
[Log] You inserted 1
[Log] You inserted 12
[Log] You inserted 123
```