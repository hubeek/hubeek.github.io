# Custom order in sorting, dutch alphabet 'ij' problem

_Status: Published_
_Created: 2020-02-03 05:59:28_
_Tags: javascript_

<code>

const compareIJ =  (x, y) => {
  var a = x.toLowerCase()
  var b = y.toLowerCase()
  // combined char i+j
  if (a.startsWith('ij') && b.startsWith('i') ) {
    return -1
  } else if (a.startsWith('ij') && b.startsWith('j')){
    return 1
  }
  if (a.startsWith('i') && b.startsWith('ij')) {
    return -1
  } else if (a.startsWith('j') && b.startsWith('ij')){
    return 1
  }


  return 0;
}

const customSort = ({data, sortBy}) => {
  const sortByObject = sortBy.reduce(
    (arr, item) => {
      arr.push(item)
      return arr
    }, [])

  return data.sort((a, b) => {
    return sortByObject.indexOf(a[0]) - sortByObject.indexOf(b[0])
  }).sort(compareIJ)
}

var items = ['wer', 'qwe','ĳsdf','lkj','fgh','asdf','bsdfs','csdf','ijsaasdf','isdf','ĳsdf', 'jsdf', 'ksdf', 'wer', 'qwe']
const dutchAlphabet = ['a','b','c','d','e','f','g','h','i','ĳ','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']

var a = customSort({data: items, sortBy: dutchAlphabet})

console.log(a)
</code>