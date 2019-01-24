<template>
  <div class="flutterModelToObject">
    <h1>Flutter JSON TO Object</h1>
    <div class="json item">
      <input v-model="className">
      <textarea v-model="json"></textarea>
    </div>
    <div class="code item">
      <pre>
class {{className}} extends Object {

{{typeString}}

{{split}}{{className}}({
{{initString}}
{{split}}});

{{split}}{{className}}.fromJson(json) {
{{fromJsonStr}}
{{split}}}

{{split}}{{className}}.toJson(json)=> {
{{fromObjectStr}}
{{split}}}
}
      </pre>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      className: "className",
      json:
        '{"str":"string","number":1.0,"boolean":true,"array":[],"map":{"a":1}}',
      fromJsonStr: "",
      typeString: "",
      initString: "",
      fromObjectStr: "",
      split: "  "
    };
  },
  methods: {
    typeFormat() {
      //     String title;
    },
    fromJsonFormat() {
      try {
        const o = JSON.parse(this.json);
        this.fromJsonStr = "";
        this.typeString = "";
        this.initString = "";
        this.fromObjectStr = "";
        for (let k in o) {
          this.fromJsonStr += `${this.split}${
            this.split
          }${k} = json['${k}'];\n`;
          this.fromObjectStr += `${this.split}${
            this.split
          }'${k}' = instance.${k};\n`;
          this.typeFormat(k, o);
          this.initString += `${this.split}${this.split}this.${k},\n`;
        }
        return t;
      } catch (e) {
        return "";
      }
    },
    typeFormat(k, o) {
      const type = typeof o[k];
      switch (type) {
        case "string":
          this.typeString += `${this.split}${this.split}String ${k};\n`;
          break;
        case "number":
          this.typeString += `${this.split}${this.split}num ${k};\n`;
          break;
        case "boolean":
          this.typeString += `${this.split}${this.split}bool ${k};\n`;
          break;
        case "object":
          if (Array.isArray(o[k])) {
            this.typeString += `${this.split}${this.split}List ${k};\n`;
          } else {
            this.typeString += `${this.split}${this.split}Map ${k};\n`;
          }
          break;
      }
    }
  },
  created() {
    this.fromJsonFormat();
  }
};
</script>

<style lang="less">
body {
  margin: 0;
  padding: 0;
}
.flutterModelToObject {
  .item {
    width: 50%;
    float: left;
    box-sizing: border-box;
    padding: 0 30px;
    text-align: left;
  }
  .json {
    input {
      margin-bottom: 10px;
      padding: 5px;
    }
    textarea {
      padding: 5px;
      width: 100%;
      height: 30vh;
    }
  }
  .code {
    pre {
      background: #f7f7f7;
      padding: 20px;
    }
  }
}
</style>
