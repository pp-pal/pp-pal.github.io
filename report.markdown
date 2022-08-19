---
layout: page
title: Report bugs
permalink: /report-bugs/
nav_order: 99
---


<style>
.form {
  background-color: #15172b;
  border-radius: 20px;
  box-sizing: border-box;
  padding: 20px;
}

.title {
  color: #eee;
  font-family: sans-serif;
  font-size: 36px;
  font-weight: 600;
  margin-top: 30px;
}

.subtitle {
  color: #eee;
  font-family: sans-serif;
  font-size: 16px;
  font-weight: 600;
  margin-top: 10px;
}

.input-container {
  height: 50px;
  position: relative;
  width: 100%;
}

.ic1 {
  margin-top: 40px;
}

.ic2 {
  margin-top: 30px;
}

.input {
  background-color: #303245;
  border-radius: 12px;
  border: 0;
  box-sizing: border-box;
  color: #eee;
  font-size: 18px;
  height: 100%;
  outline: 0;
  padding: 16px 16px 0;
  width: 100%;
}

.cut {
  background-color: #15172b;
  border-radius: 10px;
  height: 20px;
  left: 20px;
  position: absolute;
  top: -20px;
  transform: translateY(0);
  transition: transform 200ms;
  width: 120px;
}

.cut-short {
  width: 50px;
}

.input:focus ~ .cut,
.input:not(:placeholder-shown) ~ .cut {
  transform: translateY(8px);
}

.placeholder {
  color: #65657b;
  font-family: sans-serif;
  left: 20px;
  line-height: 14px;
  pointer-events: none;
  position: absolute;
  transform-origin: 0 50%;
  transition: transform 200ms, color 200ms;
  top: 20px;
}

.input:focus ~ .placeholder,
.input:not(:placeholder-shown) ~ .placeholder {
  transform: translateY(-30px) translateX(10px) scale(0.75);
}

.input:not(:placeholder-shown) ~ .placeholder {
  color: #808097;
}

.input:focus ~ .placeholder {
  color: #dc2f55;
}

.submit {
  background-color: #08d;
  border-radius: 12px;
  border: 0;
  box-sizing: border-box;
  color: #eee;
  cursor: pointer;
  font-size: 18px;
  height: 50px;
  margin-top: 38px;
  text-align: center;
  padding-left: 2%;
  padding-right: 2%;
}

.submit:active {
  background-color: #06b;
}

/* Select : start */
.select {
  display:flex;
  flex-direction: column;
  position:relative;
  height:40px;
  margin: 8px 0 8px 0;
}

.option {
  padding:0 30px 0 10px;
  min-height:40px;
  display:flex;
  align-items:center;
  background:#303245;
  border-top:#222 solid 1px;
  position:absolute;
  top:0;
  width: 100%;
  pointer-events:none;
  order:2;
  z-index:1;
  transition:background .4s ease-in-out;
  box-sizing:border-box;
  overflow:hidden;
  white-space:nowrap;
  border-radius: 12px;
}

.option:hover {
  background:#303245;
}

.select:focus .option {
  position:relative;
  pointer-events:all;
}

input {
  opacity:0;
  position:absolute;
  left:-99999px;
}

input:checked + label {
  order: 1;
  z-index:2;
  background:#303245;
  border-top:none;
  position:relative;
}

input:checked + label:after {
  content:'';
  width: 0; 
	height: 0; 
	border-left: 5px solid transparent;
	border-right: 5px solid transparent;
	border-top: 5px solid white;
  position:absolute;
  right:10px;
  top:calc(50% - 2.5px);
  pointer-events:none;
  z-index:3;
}

input:checked + label:before {
  position:absolute;
  right:0;
  height: 40px;
  width: 40px;
  content: '';
  background:#303245;
}
/* Select : end */
</style>

<form class="form mx-auto width-90" id="form">
    <div class="title">Bug reporting</div>
    <div class="subtitle">Thank you for caring our products.</div>
    <div class="input-container ic1">
        <textarea id="description" class="input" placeholder=" "></textarea>
        <div class="cut"></div>
        <label class="placeholder">How did it happen?</label>
    </div>
    <div class="select" tabindex="1">
        <input class="apps" type="radio" value="Focus tabs" id="opt1" name="apps" checked>
        <label for="opt1" class="option">Focus tabs</label>
        <input class="apps" type="radio" value="Lazy chatters" id="opt2" name="apps">
        <label for="opt2" class="option">Lazy chatters</label>
    </div>
    <button type="submit" class="submit">Send bug report</button>
</form>

<script >
let url = "https://docs.google.com/forms/d/e/1FAIpQLSe5EfFcLfAzT2zGUK46bmd53OmnyGtzr1DXR4aa51j0qcREMA/formResponse";
let form = document.querySelector("#form");
form.addEventListener("submit", (e)=>{
    e.preventDefault();
    fetch(url,{
        method: "POST",
        mode: "no-cors",
        header:{
            'Content-Type': 'application/json'
            },
        body: getInputData()
    })
    .then(data=>{
        window.location.href = "/bug-report-sent";
    })
});
function getInputData(){
    let dataToPost = new FormData();
    let desctiption = document.querySelector("#description").value;
    dataToPost.append("entry.2087769879", desctiption);
    let apps = document.querySelectorAll(".apps:checked")[0].value;
    dataToPost.append("entry.417405081", apps);
    return dataToPost;
}
</script>