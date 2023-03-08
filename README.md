# -Infix-to-Postfix
Input: str = "a+b*(c^d-e)^(f+g*h)-i"
Output: abcd^e-fgh*+^*+i-
Explanation:
After converting the infix expression 
into postfix expression, the resultant 
expression will be abcd^e-fgh*+^*+i-

class Solution {
    // Function to convert an infix expression to a postfix expression.
    public static String infixToPostfix(String exp) {
         StringBuilder str=new StringBuilder("");
        Stack<Character> stack=new Stack<>();
        HashMap<Character, Integer> map=new HashMap<>();
        map.put('+',1);
        map.put('-',1);
        map.put('*',2);
        map.put('/',2);
        map.put('^',3);
        for(int i=0;i<exp.length();i++)
        {
            if((exp.charAt(i)>='a'&&exp.charAt(i)<='z')||(exp.charAt(i)>='A'&&exp.charAt(i)<='Z'))
            str.append(exp.charAt(i));
            else
            {
                char curr=exp.charAt(i);
                if(stack.isEmpty()||curr=='(')
                stack.push(curr);
                else if(curr==')')
                {
                    while(stack.peek()!='(')
                    str.append(stack.pop());
                    stack.pop();
                }
                else
                {
                    while(!stack.isEmpty()&&stack.peek()!='('&&map.get(stack.peek())>=map.get(curr))
                    str.append(stack.pop());
                    stack.push(curr);
                }
            }
        }
        while(!stack.isEmpty())
        str.append(stack.pop());
        return str.toString();
    }
}
