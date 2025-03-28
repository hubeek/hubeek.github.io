# random int between

_Status: Published_
_Created: 2015-02-08 15:12:45_
_Tags: java_

<code>
private int randInt(int min, int max) {

  Random rand = new Random();
  int randomNum = rand.nextInt((max - min) + 1) + min;

  return randomNum;
}
</code>