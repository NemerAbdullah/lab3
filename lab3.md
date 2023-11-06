

A failure-inducing input for the buggy program:
~~~
  @Test
  public void testReverseInPlaceError()
  {
    int[] input1 = { 3,2,1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1,2,3 }, input1);
  }
~~~
An input that doesn’t induce a failure:
~~~
  @Test
  public void testReverseInPlaceNoError()
  {
    int[] input1 = { 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1 }, input1);
  }
~~~
The symptom, as the output of running the tests:

![Image](Code_GVyt5fbfZ0.png)

Note: the output array is {1,2,1}

The bug, as the before-and-after code change required to fix it:

Before:
~~~
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
~~~
After:
~~~
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
      
    }
  }
~~~
