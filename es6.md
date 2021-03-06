1. Arrow Functions 
- 기존 function 개선 
- "=>"를 이용해서 코드를 용이성↑
예) const hearts2 = names.map(item => {
    return item+"♡";
});
- implicit return : 같은 줄에 뭘 적던지 간에 return 
예) const hearts = names.map(item => item+"♡"); 
- this 키워드 이벤트할 수 없음(window 가르킴) > 밖에서도 window 참조

2. Arrow Function 활용(Arrays) 
- find : 제공되는 테스트 조건을 만족하는 첫번째 엘리먼트 값을 리턴하는 함수
예) const foundMail = email.find(item => true);
const foundMail = email.find(item => item.includes("@gmail.com")); 
- filter : 제공된 함수의 조건을 만족한 모든 엘리먼트로 새로운 array를 만듬
예) const noGmail = email.filter(potoato => !potoato.includes("@gmail"));
- map : forEach지만 반환된 element들도 새로운 array를 만듬 
예) const cleaned = email.map(a => a.split("@")[0]);
- implicit return은 {}을 쓰면 사용하지 못하고 ()을 같이 쓰면 Object도 리턴 가능
예) const cleaned = email.map((a,index) => *({
    username : a.split("@")[0], 
    index // == index : index
})); 

3. Default Value
- string, number, array 등의 모든 데이터 타입 지정 가능 
예) const sayHi = (aName = "anyone") => "hello "+ aName;  

4. template literal 
- string을 연결 시 [+,"]로 쓰기 때문에 문장이 길어지고 지저분해짐 >> 이걸 개선하기 위해 나옴 
- 연결하려고 하는 string들의 시작과 끝에 `를 명시, 받은 데이터는 ${}안에 넣어서 데이터 출력 
예) const sayHi = (aName = "anyone") => `hello ${aName}`
- ${} : 표현식도 가능 예) 60*1000

5. html fragments 
- html을 추가할 때도 간편하게 `를 이용해서 html 추가 가능 
예) const addWelcome = () =>{
    const div = `
    <div class="hello">
        <h1 class="title">Hello</h1>
    </div>
    `;
    wrapper.innerHTML = div;
}
- ``사이에 줄바꿈도 인식 

6. styled components 
- 리액트를 위한 라이브러리 
- literal template를 이용하여 해당되는 태그에 css를 한꺼번에 적용 가능 
- ()를 입력하지 않고도 ``만으로도 함수 실행 가능하며, function안에 function을 적용해서 css 적용 
예) const styled = (aElement) => {
    const el = document.createElement(aElement); 
    return (args) => { //function안에 function 호출
        const styles = args[0];
        el.style=styles; //element style 
        return el;
    }; 
}; 
const title = styled("h1")`
    background-color: red;
    color:blue;
`;  

7. String Improvements 
- include : 찾고 싶은 문자가 있는지 확인 
- repeat : 원하는 글자 반복 
- startWidth : 시작 단어 확인용. 
- endsWidth : 끝 단어 확인용. 주로 이메일에서 .com있는지 유효성 검사 

8. Array Improvements 
- Array.of : 값만으로 배열을 만듬. 값이 많을 때 유용 
예) const friends2 = Array.of("nico", "lynn", "dal", "mark"); 
- Array.form : array-like object를 array로 반환 
예) const buttons = document.querySelectorAll("button"); //array가 아님. array-like object 예) HTML COLLECTION  
Array.from(buttons).forEach(button =>{ //forEach 함수가 되지 않음
    button.addEventListener("click", () => console.log("I ve been clicked"));
});
- Array.find : 조건에 맞으면, 첫번째 값을 리턴 
- Array.findIndex : 인덱스 반환 
- Array.fill : start와 end까지 원하는 string으로 채움 

9. Objct Destructuring 
* destructuring(비구조화) : object나 array 그 외 요소들 안의 변수를 바깥으로 끄집어 내서 사용할 수 있도록 하는거 
- 큰 오브젝트에서 특정 변수나 그 안에 속한 작은 오브젝트에 접근할 수 있도록 해줌 
- {} : const 변수를 생성
예) const settings = {
    notification:{
        follow: true, 
        alerts: true,
        unfollow: false  
    },
    color: {
        theme: "dark"
    }
}
const {notification} = settings; 
- object안에 object로 접근할 시, object:{object}로 접근
- default : object=false 형태로 디폴트 지정(지정을 안하면 undefined)
            부모 object가 통째로 없다고 하면 {} 
예) const {notification: {follow = false} = {}} = settings //one-line-statement 
- 최종적으로 접근하는 값만 js에서 object 바깥으로 꺼내 쓸 수 있음 

10. array destructruring 
- 데이터를 조작하지 않을 때 유용(데이터를 조작할 때는 object가 낫음)
- object와는 비슷하나 {}(중괄호) 대신 [](대괄호)로 표현
예) const days =  ["Mon", "Tue", "Wed", "Thu", "Sat", "Sun"]; 
const [mon, tue, wed, thu = "Thu"] = days;
- function 사용 가능 
예) const days = () => ["Mon", "Tue", "Wed", "Thu", "Sat", "Sun"]; 
const [mon, tue, wed, thu = "Thu"] = days();

11. Renaming 
- rest api로 받은 데이터 변수명을 바꿀 때 유용하게 쓸 수 있음
- :으로 간단하게 renaming할 수 있음 
- let도 사용가능. let을 사용할 때는 시작과 끝에 ()을 넣음
예) const settings2 = {
    color:{
        chosen_color : "dark"
    }
};

let chosenColor = "blue";
({color:{chosen_color : chosenColor = "light"}} = settings2); 

12. Function Destructuring 
- 함수에 여러개의 파라미터를 넣으면 코드가 길어지고 지저분해지므로 object destructring을 이용하여 코드가 간편해짐
- object안에 property가 없을 경우에는 디폴트값을 명시하여 에러 없이 함수 실행 가능 
예) function saveSettings({follow, alert, color="blue"}){
    console.log(color); 
}

saveSettings({
    follow:true, 
    alert:true, 
    mkt:true
})

13. Value Shorthands(변수명 단축) 
- property의 키와 값 이름이 동일하면 키:값을 명시하지 않고도 js에서 인식 가능 
- 키와 값을 다르게 지정해도 됨 
예) const settings4 ={
    notifications:{
        follow, // == follow: follow
        alert   // == alert: alert
    }
}

14. Swapping and Skipping 
- Swapping : array destructuring을 이용하여 swapping 
예) [sat, mon] = [mon, sat]; 
- Skipping : array destructuring을 이용하여 skipping 
예) const [,,,thu, fri] = days2;

15. Spread 
- 변수를 가져가서 풀어해친다(unpack)
- ...을 이용하여 object나 array를 합침 
- 위치 아무 상관 없음 
예) const numbers = [1,2,3,4]; 
const alpabets = ["a", "b", "c"]; 
//console.log([...numbers, ...alpabets]);

const a = {
    name : "nico", 
    age : 24
}; 
const hello ={
    name : "lynn", 
    hello : "hello"
}; 
//console.log({...a, ...hello});
- 기존데이터를 복사해서 새로운 데이터를 만들 때 사용 
예) const first = ["mon", "tue", "wed"]; 
const weekend = ["sat","sun"]; 
const fullWeek = [...first , "thu", "fri", ...weekend]; 
- 선택적인 속성값(optional object property)도 지정 가능
예) const user = {
    username : "nico", 
    age : 24,
    ...(lastName !== "" && {lastName}) //spread로 전개하려면 데이터가 object여야 하므로 중괄호로 감쌈
    //lastName: lastName !== "" ? lastName : undefined
}; 

16. Rest Prameters 
- speread와는 다르게 모든 값을 하나의 변수로 축소(cotract)
- 여러개의 파라미터를 다 적기보다는 rest를 이용해서 파라미터를 다 적지 않고도 포함시킬 수 있음
- ...rest >> rest는 아무거나 써도 됨  
예) const killPassword = ({password, ...rest}) => rest; 
- spread와 쓰는 형식은 차이 없으나 파라미터 위치면 rest 
- rest는 array를 만듬 

17. For of 
- 형태 for(const dd of Array) 
예) for(const friend of friend5){
   if(friend === "Dal"){
       break;
   }else{
       console.log(friend);
   }
}
- array, Iterables, NodeList, Strings 등의 Iterable한 모든 것들에 동작 [상세](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
- const, let 모두 사용 가능 
- 루프를 사용하거나 멈춤도 가능 

18. Promise 
- 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타냄. [상세](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- 상태 : 대기(pending), 성공(fullfilled), 실패(rejected)
- 핵심) 아직 모르는 value와 함께 작업할 수 있게 해줌
* 비동기성(async) : 순차적으로 처리되는 게 아니라 한꺼번에 실행 >> js는 동시에 많은 일들을 할 수 있으며, 실행을 막지 X 
  Promise는 async를 토대로 구현 
* SetTimeOut : 일정 시간이 지난 후에 함수를 실행 <> setInterval : 일정 시간 간격을 두고 함수를 실행 
- then : promise의 결과값 반환(=언제 끝나는 건 중요하지 않고 promise가 끝났을 때 값을 돌려달라고 명령어를 내림)
         function도 넣어줄 수 있음 
         예) const thenFn = value => console.log(value); 
             amISexy.then(thenFn); // == amISexy.then(result => console.log(result))
- catch : then과 비슷하나 promise나 function에서 에러가 발생할 경우, 그 에러를 잡아 에러를 보여줌 <> uncaught : 아무도 잡지 못한 에러 >> catch로 잡아야됨 
        예) amISexy
            .then(result => console.log(result))
            .catch(error => console.log(error));
* then, catch는 각기 다른 상황에서 발생. then이 실행되면 catch는 절대 실행X(반대 경우도 동일)
- chaining promise : 여러개의 promise를 사용해서 결과값들을 가져올 때 연결
                     연결된 then은 서로의 순서가 끝나기만을 기다리고 그 결과값을 이용하여 다음 비동기 작업을 실행 
                     then은 몇개든 상관없이 연결이 가능하고 return값만 정해주면 됨  
                     예) const timesTow = (number) => number * 2; 
                        amISexy
                        .then(timesTow)
                        .then(timesTow)
                        .then(timesTow)
                        .then(timesTow)
                        .then(() => {
                            throw Error("something is wrong");
                        }) // 중간에 에러가 발생할 경우, catch로 잡아냄 
                        .then(lastNumber => console.log(lastNumber))
                        .catch(error => console.log(error));
- Promise.all : 주어진 모든 promise를 실행한 후 진행되는 하나의 promise를 반환 
                모든 값을 얻을 때까지 기다렸다가 제공. 만약에 한개의 promise가 reject가 되면 Promise.all은 reject로 반환 
                n개의 promise를 지정했을 때, 프로세스가 제대로 돌아가는지를 확인하는데 유용 
                예) const p2 = new Promise((resolve, reject) =>{
                        setTimeout(resolve, 1000, "Second");
                    }); 

                    const p3 = new Promise((resolve) =>{
                        setTimeout(resolve, 3000, "Third");
                    }); 

                    const motherPromise = Promise.all([p2,p3]); //내가 정한 순서대로 기다렸다가 하나의 값을 제공. promise들이 얼마나 걸리든지 상관없이 
                    motherPromise.then(values => console.log(values)).catch(error => console.log(error)); //array로 결과 반환
- Promise.race : n개의 promise 중에 하나라도 resolve나 reject가 되면, 빠른 결과를 보여줌. 
                 어느 것이 먼저 되는지 상관 없을 때 race를 사용
                 all과 사용법은 동일  
                 예) const motherPromise = Promise.race([p2,p3]); 
- finally : 성공하든 실패하든 상관없이 나옴
            예) const p1 = new Promise((resolve, reject) =>{
                    setTimeout(reject, 10000, "First");
                })
                .then(value => console.log(value))
                .catch(error => console.log(`${error}`))
                .finally(() => console.log("Im done"));
- 다른 사이트의 api를 이용하여 데이터를 가져올 때, promise를 사용 
예) fetch("https://yts.mx/api/v2/list_movies.json")
.then(response => {
    console.log(response); 
    return response.json(); 
}) // 다른 promise를 리턴(response.text()), response.json()도 가능
.then(json => console.log(json)) // 그 promise를 받아서 console.log
.catch(e => console.log(`＊ ${e}`));
* fetch : 데이터를 가져올 때, 사용되며 Promise를 return 

19. aysnc / await
- promise의 업데이트 버전 
- await : 항상 aysnc 함수 내에서만 사용 가능 >> async를 지우면 에러 발생
          기본적으로 Promise가 끝날때까지(resolve, reject 상관없이) 기다렸다가 반환된 promise를 받음 
          arrow function == async function 함수명(){} 
          예) const getMoviesAsync = async() =>{  
                const response = await fetch("https://yts.mx/api/v2/list_movies.json");
                console.log(response);   
            }
- try ~ catch ~ finally : 기존 다른 언어에 있던 방식과 비슷
                          catch 블락은 try블락에 발생하는 await든 밖에 에러든 상관없이 발생하면 잡아냄
예) const getMoviesAsync = async() =>{ 
    try{
        const response = await fetch("https://yts.mx/api/v2/list_movies.json"); 
        const json = await response.json();
        //throw Error("Im hungry");
        console.log(json);
    }catch(e){
        console.log(e);
    }finally{
        console.log("We are done");
    }
}
- parallel asnync await도 가능 
예) const getMoviesAsync = async() =>{  
    try{
        const [moviesResponse, suggestionsResponse] = await Promise.all([
            fetch("https://yts.mx/api/v2/list_movies.json"), 
            fetch("https://yts.mx/api/v2/movie_suggestions.json?movie_id=100")
        ]); //api로 받은 데이터들을 destructuring 

        const [movies, suggestions] = await Promise.all([
            moviesResponse.json(), 
            suggestionsResponse.json()
        ]);
        console.log(movies, suggestions);
    }catch(e){
        console.log(e);
    }finally{
        console.log("We are done");
    }
} 
* aysnc /await 말고도 axios(액시오스) 방법도 있음 

