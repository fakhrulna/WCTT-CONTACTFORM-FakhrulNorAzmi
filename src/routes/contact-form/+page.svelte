<script>
  import { onMount } from 'svelte';
  
      import { form } from './store'
      
      let formValues = {
          name: '',
          email: '',
          desc: ''
      }
  
      let alertm = 'hide'
  
      const addToArray = () => {
          if (formValues.name != '' && formValues.email != '' && formValues.desc != '') {
              // @ts-ignore
              form.update(oldForm => [...oldForm, formValues])
              submitForm()
          }
      };
  
      function submitForm() {
        alertm = 'show'
      }
  
      // const submitForm = async () =>  {
      //   // const res = await fetch(`http://localhost:8080/contact/create?name=`+formValues.name+`&email=`+formValues.email+`&description=`+formValues.desc, {
      //   //   method: "POST",
      //   // });
      // // const weather = await res.json()
      // // return { body: weather }
      //   const submit = await fetch("http://localhost:8080/contact/create", {
      //     method: "POST",
      //     body: JSON.stringify(formValues),
      //   })
      // }
  </script>
  
  {#if alertm == 'show'}
  <div class="alert success">
    <span class="closebtn" on:click={() => {alertm = 'hide'}}>&times;</span> 
    <strong>Success.</strong> Your form already submitted
  </div>
  {/if}
  <form class="w-full max-w-xl mx-auto mt-20 bg-gray-200 shadow-xl" action="http://localhost:8080/contact/create" method="post" on:submit={() => submitForm()}>
    <div class="">
      <h1 class="mx-auto w-max text-4xl font-bold">Contact Us</h1>
    </div>
    <div class="flex flex-wrap mx-3 mb-6 pt-10">
      <div class="w-full">
        <label for="name" class="text-xl">Fullname</label>
        <input id="name" name="name" type="text" class="w-full py-2 px-3" bind:value={formValues.name} required/>
      </div>
    </div>
    <div class="flex flex-wrap mx-3 mb-6">
      <div class="w-full ">
        <label for="email" class="text-xl">Email</label>
        <input id="email" name="email" type="email" class="w-full py-2 px-3" bind:value={formValues.email} required/>
      </div>
    </div>
    <div class="flex flex-wrap mx-3 mb-6 pb-10">
      <div class="w-full ">
        <label for="desc" class="text-xl">Description</label>
        <textarea id="desc" name="description" cols="30" rows="5" class="w-full py-2 px-3" bind:value={formValues.desc} required></textarea>
      </div>
    </div>
    <div class="flex flex-wrap mx-3 mb-6 pb-10">
      <div class="w-full ">
        <button class="btn info" type="submit">Submit</button>
      </div>
    </div>
  </form>
  
  <style>
  .btn {
    border: none;
    color: white;
    padding: 14px 28px;
    font-size: 16px;
    cursor: pointer;
  }
  
  .info {background-color: #2196F3;} /* Blue */
  .info:hover {background: #0b7dda;}
  
  .alert {
    padding: 20px;
    background-color: #04AA6D;
    color: white;
  }
  
  .closebtn {
    margin-left: 15px;
    color: white;
    font-weight: bold;
    float: right;
    font-size: 22px;
    line-height: 20px;
    cursor: pointer;
    transition: 0.3s;
  }
  
  .closebtn:hover {
    color: black;
  }
  </style>