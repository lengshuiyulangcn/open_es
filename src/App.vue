<template>
  <div id="app" class="container">
    <img src="./assets/logo.png">
    <div class="row">
      <div class="col-md-12">
				<div class="bs-callout bs-callout-success">
					<h4>标题要醒目</h4>
						{{origin}}
				</div>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6">
        <Editor :content="content" @input="update"></Editor>
      </div>
      <div class="col-md-6">
				<Sheet :content="content"></Sheet>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <button type='submit' class="btn btn-success long-btn">提交修改</button>
      </div>
    </div>
  </div>
</template>

<script>
import Sheet from './components/Sheet'
import Editor from './components/Editor'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import * as differ from 'diff'

var origin = 'Rails Girls 项目是一个免费的公益活动，我们提供为时1天的Web开发入门课程，我们为女性提供工具，帮助她们更好地认识编程艺术，掌握Ruby on Rails技术，并在最快的时间内实施你的想法。Rails Girls起源于芬兰，目前为止，Rails Girls 已经在全球很多国家成功地组织了工作坊。'
export default {
  name: 'app',
  data () {
    return {content: origin, origin: origin}
  },
  components: {
    Sheet,
    Editor
  },
  methods: {
    update (message) {
      var diff = differ.diffChars(origin, message)
      let result = ''
      diff.forEach(function (part) {
        if (part.removed) {
          result += `<span style="text-decoration: line-through; font-style: italic; color: red;">${part.value}</span>`
        } else if (part.added) {
          result += `<span style="color: green;">${part.value}</span>`
        } else {
          result += part.value
        }
      })
      result = `<p>${result}</p>`
      this.content = result
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.long-btn {
  margin-top: 30px;
  width: 100%;
}
.bs-callout {
    padding: 20px;
    margin: 20px 0;
    border: 1px solid #eee;
    border-left-width: 5px;
    border-radius: 3px;
	  text-align: left;
}
.bs-callout h4 {
	  text-align: left;
    margin-top: 0;
    margin-bottom: 5px;
}
.bs-callout p:last-child {
    margin-bottom: 0;
}
.bs-callout code {
    border-radius: 3px;
}
.bs-callout+.bs-callout {
    margin-top: -5px;
}
.bs-callout-default {
    border-left-color: #777;
}
.bs-callout-default h4 {
    color: #777;
}
.bs-callout-primary {
    border-left-color: #428bca;
}
.bs-callout-primary h4 {
    color: #428bca;
}
.bs-callout-success {
    border-left-color: #5cb85c;
}
.bs-callout-success h4 {
    color: #5cb85c;
}
.bs-callout-danger {
    border-left-color: #d9534f;
}
.bs-callout-danger h4 {
    color: #d9534f;
}
.bs-callout-warning {
    border-left-color: #f0ad4e;
}
.bs-callout-warning h4 {
    color: #f0ad4e;
}
.bs-callout-info {
    border-left-color: #5bc0de;
}
.bs-callout-info h4 {
    color: #5bc0de;
}
</style>
