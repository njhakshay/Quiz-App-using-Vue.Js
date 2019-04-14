<template>
    <div>
         <b-nav>
    <b-nav-item disabled><b>Quiz App</b></b-nav-item>
    <b-nav-item disabled><b>Marks Obtained</b> {{noCorrect}}/{{noTotal}}</b-nav-item>
  </b-nav>
    </div>
</template>

<script>
export default {
  props:[
    'noCorrect',
    'noTotal'
  ]
}
</script>
