<script src="https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/3.2.2/swagger-ui-bundle.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/3.2.2/swagger-ui-standalone-preset.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>


<template>
    <div id="app">
        <div id="swagger-ui"></div>
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
             style="position:absolute;width:0;height:0">
            <defs>
                <symbol viewBox="0 0 20 20" id="unlocked">
                    <path d="M15.8 8H14V5.6C14 2.703 12.665 1 10 1 7.334 1 6 2.703 6 5.6V6h2v-.801C8 3.754 8.797 3 10 3c1.203 0 2 .754 2 2.199V8H4c-.553 0-1 .646-1 1.199V17c0 .549.428 1.139.951 1.307l1.197.387C5.672 18.861 6.55 19 7.1 19h5.8c.549 0 1.428-.139 1.951-.307l1.196-.387c.524-.167.953-.757.953-1.306V9.199C17 8.646 16.352 8 15.8 8z"></path>
                </symbol>

                <symbol viewBox="0 0 20 20" id="locked">
                    <path d="M15.8 8H14V5.6C14 2.703 12.665 1 10 1 7.334 1 6 2.703 6 5.6V8H4c-.553 0-1 .646-1 1.199V17c0 .549.428 1.139.951 1.307l1.197.387C5.672 18.861 6.55 19 7.1 19h5.8c.549 0 1.428-.139 1.951-.307l1.196-.387c.524-.167.953-.757.953-1.306V9.199C17 8.646 16.352 8 15.8 8zM12 8H8V5.199C8 3.754 8.797 3 10 3c1.203 0 2 .754 2 2.199V8z"/>
                </symbol>

                <symbol viewBox="0 0 20 20" id="close">
                    <path d="M14.348 14.849c-.469.469-1.229.469-1.697 0L10 11.819l-2.651 3.029c-.469.469-1.229.469-1.697 0-.469-.469-.469-1.229 0-1.697l2.758-3.15-2.759-3.152c-.469-.469-.469-1.228 0-1.697.469-.469 1.228-.469 1.697 0L10 8.183l2.651-3.031c.469-.469 1.228-.469 1.697 0 .469.469.469 1.229 0 1.697l-2.758 3.152 2.758 3.15c.469.469.469 1.229 0 1.698z"/>
                </symbol>

                <symbol viewBox="0 0 20 20" id="large-arrow">
                    <path d="M13.25 10L6.109 2.58c-.268-.27-.268-.707 0-.979.268-.27.701-.27.969 0l7.83 7.908c.268.271.268.709 0 .979l-7.83 7.908c-.268.271-.701.27-.969 0-.268-.269-.268-.707 0-.979L13.25 10z"/>
                </symbol>

                <symbol viewBox="0 0 20 20" id="large-arrow-down">
                    <path d="M17.418 6.109c.272-.268.709-.268.979 0s.271.701 0 .969l-7.908 7.83c-.27.268-.707.268-.979 0l-7.908-7.83c-.27-.268-.27-.701 0-.969.271-.268.709-.268.979 0L10 13.25l7.418-7.141z"/>
                </symbol>


                <symbol viewBox="0 0 24 24" id="jump-to">
                    <path d="M19 7v4H5.83l3.58-3.59L8 6l-6 6 6 6 1.41-1.41L5.83 13H21V7z"/>
                </symbol>

                <symbol viewBox="0 0 24 24" id="expand">
                    <path d="M10 18h4v-2h-4v2zM3 6v2h18V6H3zm3 7h12v-2H6v2z"/>
                </symbol>
            </defs>
        </svg>
    </div>
</template>

<script>
  // import HelloWorld from './components/HelloWorld.vue'
  import jsyaml from 'js-yaml';

  export default {
    name: 'app',
    // components: {
    //   HelloWorld
    // },

    async mounted() {

      const script = document.createElement("script");
      script.src = "https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/3.2.2/swagger-ui-bundle.js";
      script.async = true;
      await document.head.appendChild(script);

      const script2 = document.createElement("script");
      script2.src = "https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/3.2.2/swagger-ui-standalone-preset.js";
      script2.async = true;
      await document.head.appendChild(script2);

      const script3 = document.createElement("script");
      script3.src = "https://unpkg.com/vue-router/dist/vue-router.js";
      script3.async = true;
      await document.head.appendChild(script3);

      const link = document.createElement('Link');
      link.href = 'https://cdnjs.cloudflare.com/ajax/libs/swagger-ui/3.2.2/swagger-ui.css';
      link.rel = 'stylesheet';
      document.head.appendChild(link);

      // console.log(this.get_url())

      // @see https://qiita.com/567000/items/dde495d6a8ad1c25fa43#fetch%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%9Fajax%E5%87%A6%E7%90%86
      // const url = this.$route.query.url;
      // console.log(url)
      const res = await fetch('https://raw.githubusercontent.com/swagger-api/swagger-samples/master/java/inflector-dropwizard/src/main/swagger/swagger.yaml')
      const res_body = await res.text();
      const swagger_json = jsyaml.load(res_body);
      console.log(swagger_json)

      const ui2 = SwaggerUIBundle({
        spec: swagger_json,
        dom_id: '#swagger-ui',
        deepLinking: true,
        presets: [
          SwaggerUIBundle.presets.apis,
          SwaggerUIStandalonePreset
        ],
        plugins: [
          SwaggerUIBundle.plugins.DownloadUrl
        ],
        layout: 'StandaloneLayout'
      })
      window.ui = ui2
    },
    methods: {
      get_url: function() {
        // @see https://stackoverflow.com/questions/35914069/how-can-i-get-query-parameters-from-a-url-in-vue-js
        let uri = window.location.href.split('?');
        if (uri.length == 2) {
          let vars = uri[1].split('&');
          let getVars = {};
          let tmp = '';
          vars.forEach(function (v) {
            tmp = v.split('=');
            if (tmp.length == 2)
              getVars[tmp[0]] = tmp[1];
          });
          return getVars.url;
        }
      },
      sample: function() {
        window.onload = function () {
          var spec = {
            'openapi': '3.0.0',
            'info': { 'version': '1.0.0', 'title': 'Swagger Petstore', 'license': { 'name': 'MIT' } },
            'servers': [{ 'url': 'http://petstore.swagger.io/v1' }],
            'paths': {
              '/pets': {
                'get': {
                  'summary': 'List all pets',
                  'operationId': 'listPets',
                  'tags': ['pets'],
                  'parameters': [{
                    'name': 'limit',
                    'in': 'query',
                    'description': 'How many items to return at one time (max 100)',
                    'required': false,
                    'schema': { 'type': 'integer', 'format': 'int32' }
                  }],
                  'responses': {
                    '200': {
                      'description': 'A paged array of pets',
                      'headers': {
                        'x-next': {
                          'description': 'A link to the next page of responses',
                          'schema': { 'type': 'string' }
                        }
                      },
                      'content': { 'application/json': { 'schema': { '$ref': '#/components/schemas/Pets' } } }
                    },
                    'default': {
                      'description': 'unexpected error',
                      'content': { 'application/json': { 'schema': { '$ref': '#/components/schemas/Error' } } }
                    }
                  }
                },
                'post': {
                  'summary': 'Create a pet',
                  'operationId': 'createPets',
                  'tags': ['pets'],
                  'responses': {
                    '201': { 'description': 'Null response' },
                    'default': {
                      'description': 'unexpected error',
                      'content': { 'application/json': { 'schema': { '$ref': '#/components/schemas/Error' } } }
                    }
                  }
                }
              },
              '/pets/{petId}': {
                'get': {
                  'summary': 'Info for a specific pet',
                  'operationId': 'showPetById',
                  'tags': ['pets'],
                  'parameters': [{
                    'name': 'petId',
                    'in': 'path',
                    'required': true,
                    'description': 'The id of the pet to retrieve',
                    'schema': { 'type': 'string' }
                  }],
                  'responses': {
                    '200': {
                      'description': 'Expected response to a valid request',
                      'content': { 'application/json': { 'schema': { '$ref': '#/components/schemas/Pets' } } }
                    },
                    'default': {
                      'description': 'unexpected error',
                      'content': { 'application/json': { 'schema': { '$ref': '#/components/schemas/Error' } } }
                    }
                  }
                }
              }
            },
            'components': {
              'schemas': {
                'Pet': {
                  'required': ['id', 'name'],
                  'properties': {
                    'id': { 'type': 'integer', 'format': 'int64' },
                    'name': { 'type': 'string' },
                    'tag': { 'type': 'string' }
                  }
                },
                'Pets': { 'type': 'array', 'items': { '$ref': '#/components/schemas/Pet' } },
                'Error': {
                  'required': ['code', 'message'],
                  'properties': { 'code': { 'type': 'integer', 'format': 'int32' }, 'message': { 'type': 'string' } }
                }
              }
            }
          }
          // Build a system
          const ui = SwaggerUIBundle({
            spec: spec,
            dom_id: '#swagger-ui',
            deepLinking: true,
            presets: [
              SwaggerUIBundle.presets.apis,
              SwaggerUIStandalonePreset
            ],
            plugins: [
              SwaggerUIBundle.plugins.DownloadUrl
            ],
            layout: 'StandaloneLayout'
          })
          window.ui = ui
        }
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

    html
    {
      box-sizing: border-box;
      overflow: -moz-scrollbars-vertical;
      overflow-y: scroll;
    }
    *,
    *:before,
    *:after
    {
      box-sizing: inherit;
    }
    body {
      margin:0;
      background: #fafafa;
    }
</style>
