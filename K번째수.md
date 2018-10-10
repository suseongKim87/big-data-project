이 문제는 array에서 commands의 [i]번째의 정보를 받아 정렬된 값에서 선택된 배열의 값을 가져오는 문제입니다.

1. commands[i][0] => 정렬하고자하는 부분의 시작위치
2. commands[i][1] => 정렬하고자하는 부분의 종료위치
3. commands[i][2] => 정렬된 값의 선택된 배열위치

배열을 sort해서 값을 가져오는 문제로 2가지 방법으로 풀어 봤습니다.
(첫번째는 list를 써서 풀어서 봤으며 System의 arraycopy로 풀었고, 두번째는 arrayOfRange를 이용해 범위를 가져와 풀었습니다.)

URL 링크: [프로그러머스 문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/42748?language=java)

```{.java}
package test;

import java.util.*;
import java.lang.*;

public class JavaTest2 {

    public static void main(String[] args) {
        for(int result : solution(new int[]{1, 5, 2, 6, 3, 7, 4}, new int[][]{{2, 5, 3}, {4, 4, 1}, {1, 7, 3}})){
            System.out.println(result);
        }
    }
    
    //리스트를 stream 함수를 이용해서 array로 반환.
    public static int[] solution1(int[] array, int[][] commands) {
        List<Integer> list = new ArrayList<>();

        for(int[] command : commands) {
            int[] value = new int[command[1]+1 - command[0]];
            System.arraycopy(array, command[0]-1, value, 0, command[1]+1 - command[0]);
            Arrays.sort(value);
            list.add(value[command[2]-1]);
        }
        return list.stream().mapToInt(i->i).toArray();
    }
    
    //array를 원하는 부분을 잘라 사용. 
    public static int[] solution2(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i=0; i<commands.length; i++) {
            int[] temp = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(temp);
            answer[i] = temp[commands[i][2]-1];
        }

        return answer;
    }
}

```
