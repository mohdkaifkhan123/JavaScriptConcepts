//Progess bar
import React, { useEffect, useState } from "react";

const ProgressBar = () => {
  const [progress, setProgress] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setProgress((prevProgress) => {
        if (prevProgress < 100) {
          return prevProgress + 1;
        } else {
          clearInterval(intervalId);
          return prevProgress;
        }
      });
    }, 100); // Increase progress every 100ms

    // Cleanup interval on component unmount
    return () => clearInterval(intervalId);
  }, []);

  return (
    <div
      style={{
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        alignItems: "center",
        height: "100vh",
      }}
    >
      <div
        style={{
          width: "500px",
          height: "30px",
          border: "2px solid black",
          backgroundColor: "#e0e0e0",
          position: "relative",
        }}
      >
        <div
          style={{
            width: `${progress}%`,
            height: "100%",
            backgroundColor: "red",
            transition: "width 0.1s linear",
          }}
        ></div>
      </div>
      <p>{progress}%</p>
    </div>
  );
};

export default ProgressBar;



//Make nested object flat
const obj={
    a:1,
    b:10,
    d:{
        e:20
    }
}
const object={}
function a(obj,parent){
    for(let key in obj){
        let newParent=parent+key
        let value=obj[key]
        console.log(value)
        if(typeof value==='object')
        {
        a(value,newParent+".")
        }
        else
        object[newParent]=value;
    }
    return object
}
console.log(a(obj,""))




//Composition in js
function add(a){
    return a+2
}
function subtract(a){
    return a-3
}
function multiply(a){
    return a*3
}

const compose=(...functions)=>{
    return(args)=>{
     return   functions.reduceRight((arg,fn)=>fn(arg),args);
    }
}

const solve=compose(add,subtract,multiply)

console.log(solve(6))





//Polyfill for array flat method
const arr=[[1,2],[1,3],[[4]]]


const result=[]

function polyfillFlatArray(arr){
    arr.forEach((item)=>{
        if(Array.isArray(item))
        polyfillFlatArray(item)
        else
        result.push(item)
    })
    return result
}

console.log(polyfillFlatArray(arr))



//Polyfill for promise.all

const d=(time)=>{
    return new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve(time)
        },time)
    })
}
const arr=[d(1000),d(2000),d(3000)]
console.log(arr)

const polyfillPromiseAll=(arr)=>{
    const o=[]
    return new Promise((resolve,reject)=>{
        arr.forEach((promise,index)=>{
            promise.then((data)=>{
                o[index]=data
                if(index===arr.length-1)
                resolve(o)
            }).catch((error)=>{
                reject(error)
            })
        })
    })
}
polyfillPromiseAll(arr).then((data)=>{
    console.log(data)
}).catch(error=>{
    console.log(error)
})


//Calculate count of total arrays
const arr=[[1,2],[1,3],[[[4]]]]


const result=[]
let c=1;
function polyfillFlatArray(arr){
    arr.map((item)=>{
        if(Array.isArray(item))
        {
        c++
        polyfillFlatArray(item)
        }
        
    })
    return c
}

console.log(polyfillFlatArray(arr))




//React lifecycle methods

import React from "react";
class Counter extends React.Component {
  componentDidMount() {
    console.log("componentDidMount");
  }
  componentDidUpdate(prevProps, prevState) {
    if (prevProps.number !== this.props.number) {
      console.log("componentDidUpdate runs");
    }
  }
  componentWillUnmount() {
    console.log("componentWillUnmount");
  }
  render() {
    return <button>{this.props.number}</button>;
  }
}
export default Counter;
import "./styles.css";
import React from "react";
import Counter from "./components/Counter";
class App extends React.Component {
  state = {
    num: 0,
  };

  handleClick() {
    this.setState((state) => ({ num: state.num + 1 }));
  }
  render() {
    return (
      <>
        <button onClick={this.handleClick.bind(this)}>ldld</button>
        <Counter number={this.state.num} />
      </>
    );
  }
}
export default App;






















JavaScript Assessment Five Explanation And Output Questions
https://docs.google.com/document/d/1Kl5D7jd2B5Tc2qKg0_rfOyR0M7klB9XKpQrYQO5BMJg/edit?usp=sharing
