# My Notes
## First impressions
*   Mounting feels like reacts but the syntax is very different 
*   Minimum amount of dom renders is handled like in the react, according to state changes (Virtual DOM)
*   Using javascript expressions is ok (like in react) inside the mustache
*   Vue has a lot to offer when it comes to handling user input, not that complicated either


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
*   We can pass an object to :class (short for v-bind:class) to dynamically toggle classes:
    <div :class="{ active: isActive }"></div>
    for multiple: 
    <div :class="[activeClass, errorClass]"></div> 
    this is also possible:
    <div :class="[{ active: isActive }, errorClass]"></div>
*   :style supports binding to JavaScript object values - it corresponds to an HTML element's style property:
    data() {
        return {
            styleObject: {
            color: 'red',
            fontSize: '13px'
            }
        }
    }
    <div :style="styleObject"></div> (looks cleaner)
*   We can bind :style to an array of multiple style objects. These objects will be merged and applied to the same element, seems useful:
    <div :style="[baseStyles, overridingStyles]"></div>

*   You can use the v-else directive to indicate an "else block" for v-if, logic behind is easy to see:
    <button @click="awesome = !awesome">Toggle</button>
    <h1 v-if="awesome">Vue is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>
*   Else if logic is also possible:
    <div v-if="type === 'A'">
        A
    </div>
    <div v-else-if="type === 'B'">
        B
    </div>
    <div v-else-if="type === 'C'">
        C
    </div>
    <div v-else>
        Not A/B/C
    </div>
*   "template" serves as an invisible wrapper, can be used to toggle a whole bunch of elements like this:
    <template v-if="ok">
    <h1>Title</h1>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    </template>

*   v-show directive only changes the display option so it still appaears on the DOM
*   v-if is lazy, waits for the condition to be true or false
*   Generally speaking, v-if has higher toggle costs while v-show has higher initial render costs. 

*   v-for is the directive to loop inside arrays and objects and render them in the DOM:
    data() {
        return {
            items: [{ message: 'Foo' }, { message: 'Bar' }]
        }
    }
    // think of this as "for each item in items" 
    <li v-for="item in items">
        {{ item.message }}
    </li>
    or include the index like this:
    <li v-for="(item, index) in items"> 
    I can even destructure like this, it's all good dawg: 
    <li v-for="({message}, index) in items"> 
    It can be use nested like this and changing "in" to "of" is totally fine:
    <li v-for="item of items">
    <span v-for="childItem in item.children">
        {{ item.message }} {{ childItem }}
    </span>
    </li>
    It's possible to  loop through objects as well:
    <li v-for="(value, key, index) in myObject">
        {{ index }}. {{ key }}: {{ value }}
    </li>
    it will repeat the template that many times, based on a range of 1...n, (starting index is 1, pay attention):
    <span v-for="n in 10">{{ n }}</span>
*   Using it v-for with template allows me to use a block of multiple elements
*   When they exist on the same node, v-if has a higher priority than v-for. That means the v-if condition will not have access to variables from the scope of the v-for. So this usage is suggested:
    <template v-for="todo in todos">
    <li v-if="!todo.isComplete">
        {{ todo.name }}
    </li>
    </template>
*   The usage ok the key attribute is very important with v-for (especially with forms). You need to let vue know that the items are not interchangeable by giving them unique values. Don't use the index because when, for example, an item is prepended it get's the first index and you will face all kinds of bugs (depending on your project). https://www.youtube.com/watch?v=lPs0uh5oR4k this helped me a lot
*   When working with non-mutating methods, we should replace the old array with the new one:
    this.items = this.items.filter((item) => item.message.match(/Foo/))
*   In situations where computed properties are not feasible (e.g. inside nested v-for loops), you can use a method:
    data() {
    return {
        sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
    }
    },
    methods: {
    even(numbers) {
        return numbers.filter(number => number % 2 === 0)
    }
    }
    <ul v-for="numbers in sets">
    <li v-for="n in even(numbers)">{{ n }}</li>
    </ul>
*   @click="handler" is shorthand for v-on:click="handler"
*   With an inline handler:   
    data() {
        return {
            count: 0
        }
    }
    <button @click="count++">Add 1</button>
    <p>Count is: {{ count }}</p>

*   v-on can also accept the name or path of a component method you'd like to call. Jsut define the function (method) you wanna call in methods so you can call directly like this, we have access to event as well: 
    methods: {
    say(message) {
        alert(message)
    }
    greet(event) {
        // `this` inside methods points to the current active instance
        alert(`Hello ${this.name}!`)
        // `event` is the native DOM event
        if (event) {
        alert(event.target.tagName)
        }
    }
    <button @click="greet">Greet</button>
    <button @click="say('bye')">Say bye</button>

*   We can reach event from an inline handler, both are valid, $event is a special variable:
    <!-- using $event special variable -->
    <button @click="warn('Form cannot be submitted yet.', $event)">
    Submit
    </button>

    <!-- using inline arrow function -->
    <button @click="(event) => warn('Form cannot be submitted yet.', event)">
    Submit
    </button>

*   There are event modifiers that is used for preventing default for submits or stop propagation:
    <!-- the click event's propagation will be stopped -->
    <a @click.stop="doThis"></a>
    <!-- the submit event will no longer reload the page -->
    <form @submit.prevent="onSubmit"></form>
    <!-- modifiers can be chained -->
    <a @click.stop.prevent="doThat"></a>
    <!-- just the modifier -->
    <form @submit.prevent></form>
    <!-- only trigger handler if event.target is the element itself -->
    <!-- i.e. not from a child element -->
    <div @click.self="doThat">...</div>

*   The .capture, .once, and .passive modifiers mirror the options of the native addEventListener method:
    <!-- use capture mode when adding the event listener -->
    <!-- i.e. an event targeting an inner element is handled here before being handled by that element -->
    <div @click.capture="doThis">...</div>
    <!-- the click event will be triggered at most once -->
    <a @click.once="doThis"></a>
    <!-- the scroll event's default behavior (scrolling) will happen -->
    <!-- immediately, instead of waiting for `onScroll` to complete  -->
    <!-- in case it contains `event.preventDefault()`                -->
    <div @scroll.passive="onScroll">...</div>

*   Key modifiers are very easy to use as well:
    <!-- only call `vm.submit()` when the `key` is `Enter` -->
    <input @keyup.enter="submit" />
*   it's easy to use any valid key names exposed via KeyboardEvent.key as modifiers by converting them to kebab-case ('PageDown' key example):
    <input @keyup.page-down="onPageDown" />

*   ctrl, alt etc. + and event is also possible:
    <!-- Alt + Enter -->
    <input @keyup.alt.enter="clear" />
    <!-- Ctrl + Click -->
    <div @click.ctrl="doSomething">Do something</div>

*   .exact listens for the exact combination:
    <!-- this will fire even if Alt or Shift is also pressed -->
    <button @click.ctrl="onClick">A</button>
    <!-- this will only fire when Ctrl and no other keys are pressed -->
    <button @click.ctrl.exact="onCtrlClick">A</button>
    <!-- this will only fire when no system modifiers are pressed -->
    <button @click.exact="onClick">A</button>

*   v-model makes it so easy to work with forms, directly gets the input and shows it on dom, can be used with textarea, radio, checkbox etc.:
    <p>Message is: {{ message }}</p>
    <input v-model="message" placeholder="edit me" />

    <!-- bad -->
    <textarea>{{ text }}</textarea>
    <!-- good -->
    <textarea v-model="text"></textarea>

*   For checkbox, alternates the checked value with ust this much code, cool:
    data() {
        return {
            checked: true
        }
    }
    <template>
    <input type="checkbox" id="checkbox" v-model="checked" />
    <label for="checkbox">{{ checked }}</label>
    </template>

*   When used with an array it just pushes the values of the checked options into the array:
      data() {
        return {
            checkedNames: []
        }
    }
    <template>
    <!--we display the array with the checked values, easy-->
    <div>Checked names: {{ checkedNames }}</div>

    <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
    <label for="jack">Jack</label>
    
    <input type="checkbox" id="john" value="John" v-model="checkedNames" />
    <label for="john">John</label>
    
    <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
    <label for="mike">Mike</label>
    </template>

*   The radio buttons and values also work in a very similar way:
    data() {
        return {
            picked: 'One'
        }
    }
    <!--picked shows the picked options-->
    <template>
        <div>Picked: {{ picked }}</div>

        <input type="radio" id="one" value="One" v-model="picked" />
        <label for="one">One</label>

        <input type="radio" id="two" value="Two" v-model="picked" />
        <label for="two">Two</label>
    </template>

*   Keep the v-model in select noot in the options:
    data() {
        return {
         selected: ''
        }
    }
    
    <template>
    <span> Selected: {{ selected }}</span>
    <!--<select v-model="selected"> -->
    <!--its  possible to use multiple options of course and the selected options would appear in array-->
    <select v-model="selected" multiple>
        <option disabled value="">Please select one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
    </select>

*   true-value and false-value are Vue-specific attributes that only works with v-model. Here the toggle property's value will be set to 'yes' when the box is checked, and set to 'no' when unchecked:
    <input
    type="checkbox"
    v-model="toggle"
    true-value="yes"
    false-value="no" />

*   pick will be set to the value of first when the first radio input is checked, and set to the value of second when the second one is checked:
    <input type="radio" v-model="pick" :value="first" />
    <input type="radio" v-model="pick" :value="second" />

*   You can add the lazy modifier to v-model instead sync after change events:
    <input v-model.lazy="msg" /> <!-- synced after "change" instead of "input" -->
*   .number automatically converts the given input to a number. The number modifier is applied automatically if the input has type="number":
    <input v-model.number="age" />
*   .trim gets rid of the whitespace:
    <input v-model.trim="msg" />

*   All lifecycle hooks are called with their **this** context pointing to the current active instance invoking it. Note this means you should avoid using arrow functions when declaring lifecycle hooks, as you won't be able to access the component instance via this if you do so. There are also other hooks which will be called at different stages of the instance's lifecycle, with the most commonly used being **mounted**, **updated**, and **unmounted**.