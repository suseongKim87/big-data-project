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
    
    public static int[] solution2(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];

        for(int i=0; i<commands.length; i++){
            int[] temp = Arrays.copyOfRange(array, commands[i][0]-1, commands[i][1]);
            Arrays.sort(temp);
            answer[i] = temp[commands[i][2]-1];
        }

        return answer;
    }
}

```
