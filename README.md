# My Notes
## First impressions
*   Mounting feels like reacts but the syntax is very different 
*   Minimum amount of dom renders is handled like in the react, according to state changes (Virtual DOM)
*   Using javascript expressions is ok (like in react) inside the mustache
## Notes
*   If you are using Vue to enhance server-rendered HTML and only need Vue to control specific parts of a large page, avoid mounting a single Vue application instance on the entire page. Instead, create multiple small application instances and mount them on the elements they are responsible for.

*   All Vue templates are syntactically valid HTML that can be parsed by spec-compliant browsers and HTML parsers.
*   Mustache "{{variable/value}}"
*   The v-html attribute you're seeing is called a directive. Directives are prefixed with v- to indicate that they are special attributes provided by Vue, and as you may have guessed, they apply special reactive behavior to the rendered DOM. 
    <p>Using text interpolation: {{ rawHtml }}</p>
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>
*   Mustaches cannot be used inside HTML attributes. Instead, use a v-bind directive: 
    <div v-bind:id="dynamicId"></div> 
    or shorthand:
    <div :id="dynamicId"></div> 
    Anothe example: 
    <button :disabled="isButtonDisabled">Button</button>
*   Functions can be called like this : 
    <span :title="toTitleDate(date)">
        {{ formatDate(date) }}
    </span>
*   A directive example that remove / insert the <p> according to the seen's value:
    <p v-if="seen">Now you see me</p>
*   v-on directive listens to DOM events:
    <a v-on:click="doSomething"> ... </a>
    <!-- shorthand -->
    <a @click="doSomething"> ... </a>
    to change the event to listen to dynamically: 
    <a @[eventName]="doSomething">
    **"eventName" will be converted to "eventname" so caps matter keep it lower case**
*   Modifier example that prevents the deafult behaviour in a form tag:
    <form @submit.prevent="onSubmit">...</form>
*   To add methods to a component instance we use the methods option. This should be an object containing the desired methods:
    methods: {
        increment() {
            this.count++
        }
    },
    avoid using arrow functions because with arrow fucntions "this" won't be referring to vue application instance

*   DOM updates are not applied synchronously. Instead, Vue buffers them until the "next tick" in the update cycle to ensure that each component needs to update only once no matter how many state changes you have made. To wait for the DOM update to complete after a state change, you can use the nextTick() global API

*   A computed property will only re-evaluate when some of its reactive dependencies have changed. The same behaviour can be achieved by using methods but the methods are not cached. A method invocation will always run the function whenever a re-render happens. To avoid cluttering use computed property:
    computed: {
        publishedBooksMessage() {
            return this.author.books.length > 0 ? 'Yes' : 'No'
        }
    }
    and use it like this:
    <span>{{ publishedBooksMessage }}</span>
*   Use getter and setters without side effects and avoid mutating the computed value.