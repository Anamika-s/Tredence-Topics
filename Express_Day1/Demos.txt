const express = require("express")
var app = express()

const port = 3000
 
// HTTP  Verbs
// get post put delete
app.get("/", (req,res)=>
{
  console.log("hello")
   
  res.send()

})
app.get("/hello", (req,res)=>
{
  res.send("Hello 1")

})


app.get("/msg", (req,res)=>
{
  res.send("Hello 2")

})
app.get("/about" ,(req,res)=>{
  res.send("About Us Page ")
})

app.get("/multiple", (req,res,next)=>
{
  console.log("some logic will come here")
  next()
} ,(req,res)=>
{
res.send("More than 1 callbacks")
})


app.post("/",(req,res)=>
{
  res.send("Record is inserted")
})

const callback1 =  (req,res,next)=>
{
  console.log("callback1")
  next()
}


const callback2 =  (req,res,next)=>
{
  console.log("callback2")
  next()
}

const callback3 =  (req,res)=>
{
  res.send("Array of functions called in response")
}
app.get("/arrayofcallbackfunctions" , [callback1,callback2,callback3] )

// combination of Indepnednt Functions & Array of functions

app.get("/combination" , [callback1, callback2] ,
(req,res,next)=>
{
  console.log("First function called")
  next()
}, (req,res)=>
{
  res.send("Last function called")
})
app.get(/a/ , (req,res)=>
{
  res.send("Path matched")
})
app.all("*", (req,res)=>
{
  res.send("There is no matching Route available")
})


app.listen(port , ()=>
{
  console.log(`Server is listening at port no ${port}`)
})
