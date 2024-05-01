# Problem
https://school.programmers.co.kr/learn/courses/30/lessons/12951

# My Solution
```
function solution(s) {
    var answer = '';
    
    if(s.length == 0) return "";
    
    s=s.split(" ");
    
    for(let i=0; i<s.length; i++) {    
        answer+=getJadenCase(s[i]);
        if(i<s.length-1) {
            answer+=" ";
        }
    }
    
    return answer;
}


const getJadenCase = (str) => {
    let answer = "";
    
    if(str.length == 0) {
        answer+=str;
    } else {
        answer+=str[0].toUpperCase();
        if(str.length>1) {
            answer+=str.substr(1, str.length).toLowerCase();
        }
    }
    
    return answer;
}
```
