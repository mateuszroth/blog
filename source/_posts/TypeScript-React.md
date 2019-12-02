---
title: TypeScript + React
tags:
  - React
  - React Hooks
  - TypeScript
categories:
  - [React, React Hooks]
  - [React, TypeScript]
date: 2019-11-01 16:13:00
---

# TypeScript Basics

## ! operator
<!--kg-card-begin: code-->

    if (a!.b!.c) { }`</pre><!--kg-card-end: code-->

    compiles to JS:
    <!--kg-card-begin: code--><pre>`if (a.b.c) { }`</pre><!--kg-card-end: code-->

    ## ? operator
    <!--kg-card-begin: code--><pre>`let x = foo?.bar.baz();`</pre><!--kg-card-end: code-->

    compiles to JS:
    <!--kg-card-begin: code--><pre>`let x = (foo === null || foo === undefined) ?
        undefined :
        foo.bar.baz();`</pre><!--kg-card-end: code-->

    And:
    <!--kg-card-begin: code--><pre>`if (someObj?.bar) {
        // ...
    }`</pre><!--kg-card-end: code-->

    is equivalent in JS to:
    <!--kg-card-begin: code--><pre>`if (someObj &amp;&amp; someObj.someProperty) {
        // ...
    }`</pre><!--kg-card-end: code-->

    TS:
    <!--kg-card-begin: code--><pre>`interface Content {
        getUrl?: () =&gt; string;
        url?: string;
    }
    interface Data {
        content?: Content;
    }
    let data: Data | undefined;
    const url: string | undefined = data?.content?.getUrl?.();
    const url2: string | undefined = data?.content?.url;`</pre><!--kg-card-end: code-->

    # Common Operators and Signatures

    ### Type intersection operator (&amp;)
    <!--kg-card-begin: code--><pre>`class WithLoading extends React.Component&lt;P &amp; WithLoadingProps&gt; { ... }`</pre><!--kg-card-end: code-->

    ### Generic function
    <!--kg-card-begin: code--><pre>`const funcComponent = &lt;P extends object&gt;(Component: React.ComponentType&lt;P&gt;): ... =&gt; { ... }`</pre><!--kg-card-end: code-->

    ### Type cast

    A type cast (props as P) is required when passing props forward from TypeScript v3.2 onwards, due to a likely bug in TypeScript.
    <!--kg-card-begin: code--><pre>`return loading ? &lt;LoadingSpinner /&gt; : &lt;Component {...props as P} /&gt;;`</pre><!--kg-card-end: code-->

    # Examples

    Worth to read:

*   about HOCs: [https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb](https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb)

    ## Higher Order Components

    ### Higher Order Component in JS
    <!--kg-card-begin: code--><pre>`const withLoading = Component =&gt;
      class WithLoading extends React.Component {
        render() {
          const { loading, ...props } = this.props;
          return loading ? &lt;LoadingSpinner /&gt; : &lt;Component {...props} /&gt;;
        }
      };`</pre><!--kg-card-end: code-->

    ### Higher Order Component in TS
    <!--kg-card-begin: code--><pre>`interface WithLoadingProps {
      loading: boolean;
    }

    const withLoading = &lt;P extends object&gt;(Component: React.ComponentType&lt;P&gt;) =&gt;
      class WithLoading extends React.Component&lt;P &amp; WithLoadingProps&gt; {
        render() {
          const { loading, ...props } = this.props;
          return loading ? &lt;LoadingSpinner /&gt; : &lt;Component {...props as P} /&gt;;
        }
      };`</pre><!--kg-card-end: code-->

    ### Function Higher Order Component in TS
    <!--kg-card-begin: code--><pre>`const withLoading = &lt;P extends object&gt;(
      Component: React.ComponentType&lt;P&gt;
    ): React.FC&lt;P &amp; WithLoadingProps&gt; =&gt; ({
      loading,
      ...props
    }: WithLoadingProps) =&gt;
      loading ? &lt;LoadingSpinner /&gt; : &lt;Component {...props as P} /&gt;;`</pre><!--kg-card-end: code-->

    ### Render Prop Component
    <!--kg-card-begin: code--><figure class="kg-card kg-code-card"><pre>`interface InjectedCounterProps {
      value: number;
      onIncrement(): void;
      onDecrement(): void;
    }

    interface MakeCounterProps {
      minValue?: number;
      maxValue?: number;
      children(props: InjectedCounterProps): JSX.Element;
    }

    interface MakeCounterState {
      value: number;
    }

    class MakeCounter extends React.Component&lt;MakeCounterProps, MakeCounterState&gt; {
      state: MakeCounterState = {
        value: 0,
      };

      increment = () =&gt; {
        this.setState(prevState =&gt; ({
          value:
            prevState.value === this.props.maxValue
              ? prevState.value
              : prevState.value + 1,
        }));
      };

      decrement = () =&gt; {
        this.setState(prevState =&gt; ({
          value:
            prevState.value === this.props.minValue
              ? prevState.value
              : prevState.value - 1,
        }));
      };

      render() {
        return this.props.children({
          value: this.state.value,
          onIncrement: this.increment,
          onDecrement: this.decrement,
        });
      }
    }`</pre><figcaption>[make-counter-render-prop.tsx](https://gist.github.com/jrwebdev/b8fea9723d4f86743c29a1888dbbe090#file-make-counter-render-prop-tsx)</figcaption></figure><!--kg-card-end: code-->

    ### Usage
    <!--kg-card-begin: code--><figure class="kg-card kg-code-card"><pre>`interface CounterProps extends InjectedCounterProps {
      style: React.CSSProperties;
    }

    const Counter = (props: CounterProps) =&gt; (
      &lt;div style={props.style}&gt;
        &lt;button onClick={props.onDecrement}&gt; - &lt;/button&gt;
        {props.value}
        &lt;button onClick={props.onIncrement}&gt; + &lt;/button&gt;
      &lt;/div&gt;
    );

    interface WrappedCounterProps extends CounterProps {
      minValue?: number;
      maxValue?: number;
    }

    const WrappedCounter = ({
      minValue,
      maxValue,
      ...props
    }: WrappedCounterProps) =&gt; (
      &lt;MakeCounter minValue={minValue} maxValue={maxValue}&gt;
        {injectedProps =&gt; &lt;Counter {...props} {...injectedProps} /&gt;}
      &lt;/MakeCounter&gt;
    );`</pre><figcaption>[wrapped-counter.tsx](https://gist.github.com/jrwebdev/c0392dfc25d3fc30893f324a89c8a16d#file-wrapped-counter-tsx)</figcaption></figure><!--kg-card-end: code-->

    ### Wrapping Render Prop as HOC
    <!--kg-card-begin: code--><pre>`import { Subtract, Omit } from 'utility-types';
    import MakeCounter, { MakeCounterProps, InjectedCounterProps } from './MakeCounter';

    type MakeCounterHocProps = Omit&lt;MakeCounterProps, 'children'&gt;;

    const makeCounter = &lt;P extends InjectedCounterProps&gt;(
      Component: React.ComponentType&lt;P&gt;
    ): React.SFC&lt;Subtract&lt;P, InjectedCounterProps&gt; &amp; MakeCounterHocProps&gt; =&gt; ({
      minValue,
      maxValue,
      ...props
    }: MakeCounterHocProps) =&gt; (
      &lt;MakeCounter minValue={minValue} maxValue={maxValue}&gt;
        {injectedProps =&gt; &lt;Component {...props as P} {...injectedProps} /&gt;}
      &lt;/MakeCounter&gt;
    );`</pre><!--kg-card-end: code-->

    Source: [https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c](https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c)

    ## React Hooks

    ### Function Components with Hooks in TS example
    <!--kg-card-begin: code--><pre>`// import useState next to FunctionComponent
    import React, { FunctionComponent, useState } from 'react';

    // our components props accept a number for the initial value
    const Counter:FunctionComponent&lt;{ initial?: number }&gt; = ({ initial = 0 }) =&gt; {
      // since we pass a number here, clicks is going to be a number.
      // setClicks is a function that accepts either a number or a function returning
      // a number
      const [clicks, setClicks] = useState(initial);
      return &lt;&gt;
        &lt;p&gt;Clicks: {clicks}&lt;/p&gt;
        &lt;button onClick={() =&gt; setClicks(clicks+1)}&gt;+&lt;/button&gt;
        &lt;button onClick={() =&gt; setClicks(clicks-1)}&gt;-&lt;/button&gt;
      &lt;/&gt;
    }
    `</pre><!--kg-card-end: code-->

    # Details about React Hooks with TypeScript

*   Examples how to use with TS: [https://fettblog.eu/typescript-react/hooks/](https://fettblog.eu/typescript-react/hooks/)
*   TS advanced: [https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d](https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d)
*   super advanced: [https://levelup.gitconnected.com/usetypescript-a-complete-guide-to-react-hooks-and-typescript-db1858d1fb9c](https://levelup.gitconnected.com/usetypescript-a-complete-guide-to-react-hooks-and-typescript-db1858d1fb9c)<!--kg-card-begin: code--><pre>`const Counter:FunctionComponent&lt;{ initial?: number }&gt; = ({ initial = 0 }) =&gt; {
      ...
    }
    `</pre><!--kg-card-end: code-->

    ### with `useState`
    <!--kg-card-begin: code--><pre>`// explicitly setting the types
    const [value, setValue] = useState&lt;number | undefined&gt;(undefined);
    const [value, setValue] = useState&lt;Array&lt;number&gt;&gt;([]);

    interface MyObject {
      foo: string;
      bar?: number;
    }
    const [value, setValue] = useState&lt;MyObject&gt;({ foo: 'hello' });
    `</pre><!--kg-card-end: code-->

    ### with `useRef`
    <!--kg-card-begin: code--><pre>`const inputEl = useRef&lt;HTMLInputElement&gt;(null);
    `</pre><!--kg-card-end: code-->

    ### with `useContext`
    <!--kg-card-begin: code--><pre>`type Theme = 'light' | 'dark';
    const ThemeContext = createContext&lt;Theme&gt;('dark');
    `</pre><!--kg-card-end: code-->

    ### with `useReducer`
    <!--kg-card-begin: code--><pre>`interface State {
      value: number;
    }

    type Action =
      | { type: 'increment' }
      | { type: 'decrement' }
      | { type: 'incrementAmount'; amount: number };

    const counterReducer = (state: State, action: Action) =&gt; {
      switch (action.type) {
        case 'increment':
          return { value: state.value + 1 };
        case 'decrement':
          return { value: state.value - 1 };
        case 'incrementAmount':
          return { value: state.value + action.amount };
        default:
          throw new Error();
      }
    };

    const [state, dispatch] = useReducer(counterReducer, { value: 0 });

    dispatch({ type: 'increment' });
    dispatch({ type: 'decrement' });
    dispatch({ type: 'incrementAmount', amount: 10 });

    // TypeScript compilation error
    dispatch({ type: 'invalidActionType' });

<!--kg-card-end: code-->

# 