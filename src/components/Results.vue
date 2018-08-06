var Results = Vue.component('results', {
  props : ["title", "description", "url", "href"],
  template: `<div>
                <div class='srch-title'>
                    {{title}}
                </div>
                <div class='srch-description'>
                    {{description}}
                </div>
                <div class='srch-url'>
                    <a :href="url">{{url}}</a>
                </div>
            </div>`
});
