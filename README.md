Prism is a lightweight, extensible syntax highlighter, built with modern web standards in mind. Today, I'll show you how you can add code highlighting in react project.
I'm assuming you've already created your React project, now let's see how we can add prismjs following these steps.

First install prismjs package with npm
npm install prismjs
Then import Prism in the component where you want to use syntax highlighting.
import Prism from "prismjs";
Then import the specific theme css that you want to use in your component. You can find all theme CSS in this path node_modules/prismjs/themes. I'm using prism-okaidia.css here.
import 'prismjs/themes/prism-okaidia.css';
After that, add the code blocks inside the pre and code tag that you want to highlight. Here className language-js is important, it will be different for other languages. You can find full language list here
<pre>
    <code className="language-js">console.log("Hello js")</code>
</pre>
Now run highlightAll in a useEffect hook to run it at the component loading time.
  useEffect(() => {
    Prism.highlightAll();
  }, []);
If you want to add any additional language that is not in prism-core than you can add them from node_modules/prismjs/components
import 'prismjs/components/prism-csharp';
If you want to use additional plugin feature like line number you can import them from here node_modules/prismjs/plugins/. I'm adding line number plugin here and line number class in <code> tag. Import JS and CSS for line numbers and className line-numbers in HTML. Find more about plugins here.
import 'prismjs/plugins/line-numbers/prism-line-numbers.js';
import 'prismjs/plugins/line-numbers/prism-line-numbers.css';
// rest of the code
<pre>
    <code className='language-js line-numbers'>{code}</code>
</pre>
Full code will look something like this
import { useEffect } from "react";
import Prism from "prismjs";
import 'prismjs/components/prism-csharp';
import 'prismjs/plugins/line-numbers/prism-line-numbers.js';
import 'prismjs/plugins/line-numbers/prism-line-numbers.css';
import 'prismjs/themes/prism-okaidia.css';

export default function Test() {
  useEffect(() => {
    Prism.highlightAll();
  }, []);
  const CsCode =
  `
  using System;
  using Alias = AnotherNamespace.SomeClass;
  namespace MyNamespace
  {
      class Program
      {
          static void Main()
          {
              AnotherNamespace.SomeClass obj1 = new AnotherNamespace.SomeClass();
              Alias obj2 = new Alias(); // Using the alias
          }
      }
  }
  `
  const JsCode =
  `const greetings ='Hello Folks';
  console.log(greetings);`

  return (
    <div className="Code">
      <h2> Code Syntax Block</h2>
      <pre>
        <code className='language-csharp line-numbers'>{CsCode}</code>
      </pre>
      <pre>
        <code className='language-js line-numbers'>{JsCode}</code>
      </pre>
    </div>
  );
}
Output:

Syntax Output
