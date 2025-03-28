# Base62 in Go

_Status: Published_
_Created: 2022-12-22 01:47:21_

The stdlib’s math/big package gives you a base62 implementation out of the box, you don’t need an external dependency for it, assuming you can hold the entire base62 dataset in memory. This is good enough for things like parsing/serializing UUIDs in a more compact format:

<code>

package main

import (
	"fmt"
	"math/big"
)

type UUID = [16]byte

func toBase62(uuid UUID) string {
	var i big.Int
	i.SetBytes(uuid[:])
	return i.Text(62)
}

func parseBase62(s string) (UUID, error) {
	var i big.Int
	_, ok := i.SetString(s, 62)
	if !ok {
		return UUID{}, fmt.Errorf("cannot parse base62: %q", s)
	}

	var uuid UUID
	copy(uuid[:], i.Bytes())
	return uuid, nil
}

func main() {
	fmt.Println(toBase62(UUID{0xFF, 0xFF, 0, 0, 0, 0, 0, 0, 0xFF, 0xFF, 0, 0, 0, 0, 0, 1}))
	fmt.Println(parseBase62("7N3zSy9F5jGaYc4BZR44Sd"))

  // Output:
  // 7N3zSy9F5jGaYc4BZR44Sd
  // [255 255 0 0 0 0 0 0 255 255 0 0 0 0 0 1] <nil>
}

</code>