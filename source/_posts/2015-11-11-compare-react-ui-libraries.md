---
layout: post
title: Compare React UI Frameworks
category: Dev
tags: [React]
---

## Intro
Got to pick a UI framework for work. The hopeful gain are unified beautiful design and quicker development. The possible loss could be performance, bugs, learning the framework, risk of unsupported in future, etc.

Where I found the candidates:

- [Existing UI libraries to use with React.js?](http://stackoverflow.com/questions/23380903/existing-ui-libraries-to-use-with-react-js)
- [awesome-react](https://github.com/enaqx/awesome-react)
- Google

I will only look at the frameworks having GitHub stars > 100.

Quick conclusion: There is no super solid framework there, but [Material UI](#material-ui) and [React toolbox](#react-toolbox) are probably more ready.

<!--more-->

## Selection criteria

- Basics: 
    + [ ] dropdownlist / select
    + [ ] date picker
    + [ ] time picker
    + [ ] tab
    + [ ] [slide in menu](http://callmenick.com/_development/slide-push-menus/)
    + [ ] dialog / modal / pop up window
    + [ ] dropdown menu
    + [ ] table
    + [ ] responsive
- Extra:
    + [ ] loading indicator
    + [ ] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [ ] theme
- [ ] tested working for new browsers (Chrome, IE11, IOS)
- [ ] use ES6 and class syntax
- [ ] compatible with React 0.14 (ref) 
- [ ] actively updated and supported
- [ ] should not have bug that broke the whole software reported in GitHub issues
- [ ] open source

## Candidates
NOTE: The GitHub data is collected on Nov 11, 2015.

- [Material UI](http://material-ui.com/#/components/appbar), [GitHub](https://github.com/callemall/material-ui), 11715 stars, 222 contributors, (22 contributors >10 commits)
- [React toolbox](http://react-toolbox.com/#/components), [GitHub](https://github.com/react-toolbox/react-toolbox), 1981 stars, 7 contributors, (3 contributors >10 commits)
- [React Bootstrap](http://react-bootstrap.github.io/components.html), [GitHub](https://github.com/react-bootstrap/react-bootstrap), 3869 stars, 127 contributors, (6 contributors >10 commits)
- [Grommet](http://www.grommet.io/docs/develop/get-started), [GitHub](https://github.com/grommet/grommet), 188 stars, 24 contributors, (8 contributors >10 commits)
- [Elemental UI](http://elemental-ui.com/home), [GitHub](https://github.com/elementalui/elemental), 1755 stars, 16 contributors
- [Belle](http://nikgraf.github.io/belle/#/component/combo-box), [GitHub](https://github.com/nikgraf/belle/), 1060 stars, 12 contributors
- [React Components by Khan Academy](http://khan.github.io/react-components/), [GitHub](https://github.com/Khan/react-components), 574 stars, 17 contributors

Not tested: 
- [TouchstoneJS](http://touchstonejs.io/), [GitHub](https://github.com/touchstonejs/touchstonejs), 2626 stars, 10 contributors. The demo and doc is under development. 
- [REACT UI](http://lobos.github.io/react-ui/), [GitHub](https://github.com/Lobos/react-ui), 294 stars, 1 contributor. Only 1 contributor, a bit worried.
- [Reapp](http://reapp.io/start.html), [GitHub](https://github.com/reapp/reapp), 2970 stars, 14 contributors. It's intended for hybrid apps, no desktop demo, lacks components.

Here are some Chinese frameworks:

- [Amaze UI] (http://amazeui.org/react/components), [GitHub](https://github.com/amazeui/amazeui-react) 474 stars, 5 contributors
- [UXCore](http://uxco.re/components/button/), [GitHub](https://github.com/uxcore)
- [Ant Design by Ant Financial (Alibaba)](http://ant.design/docs/introduce), [GitHub](https://github.com/ant-design/ant-design), 1549 stars, 36 contributors

## Go through

<a name="material-ui"></a>
### Material UI

- [material-ui](http://material-ui.com/#/components/appbar) 
- [GitHub](https://github.com/callemall/material-ui)
- 11715 stars, 222 contributors

- Basics: 
    + [X] dropdownlist / select
    + [X] date picker
    + [X] time picker
    + [X] tab
    + [X] slide in menu
    + [X] dialog / modal / popup window
    + [X] dropdown menu
    + [X] table
    + [X] responsive
- Extra:
    + [X] loading indicator
    + [ ] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [X] theme (**partly support**)
- [X] tested working for new browsers (Chrome, IE11, IOS) ([**ripple effect appear twice in iPhone**](https://github.com/callemall/material-ui/issues/1563), ripple effect not working in IE 11)
- [ ] use ES6 and class syntax 
- [X] compatible with React 0.14
- [X] actively updated and supported
- [X] should not have major bug reported in GitHub issues ()
- [X] open source

This is almost the most popular one, and it looks really beautiful with material design.  

<a name="react-toolbox"></a>
### React toolbox 

- [React toolbox](http://react-toolbox.com/#/components) 
- [GitHub](https://github.com/react-toolbox/react-toolbox) 
- 1981 stars, 7 contributors

- Basics: 
    + [X] dropdownlist / select
    + [X] date picker
    + [X] time picker
    + [X] tab
    + [X] slide in menu
    + [X] dialog / modal / popup window
    + [X] dropdown menu
    + [X] table
    + [X] responsive (**not sure**)
- Extra:
    + [ ] loading indicator
    + [X] dropdownlist / select with search/filter function (autocomplete)
    + [X] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [X] theme (**partly supported**)
- [ ] tested working for new browsers (Chrome, IE11, IOS) (**"Autocomplete" page's playground will get 'TypeError' using IE 11**) 
- [X] use ES6 and class syntax 
- [ ] compatible with React 0.14 (**not sure**)
- [X] actively updated and supported 
- [X] should not have major bug reported in GitHub issues
- [X] open source

Material Design, CSS Modules, ES6 syntax, seems promising.

<a name="react-bootstrap"></a>
### React Bootstrap
- [React Bootstrap](http://react-bootstrap.github.io/components.html) 
- [GitHub](https://github.com/react-bootstrap/react-bootstrap) 
- 3869 stars, 127 contributors

- Basics: 
    + [ ] dropdownlist / select
    + [ ] date picker
    + [ ] time picker
    + [X] tab
    + [ ] slide in menu
    + [X] dialog / modal / popup window
    + [ ] dropdown menu
    + [ ] table
    + [ ] responsive (not sure)
- Extra:
    + [ ] loading indicator
    + [ ] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [ ] theme  
(**the following is not tested due to too few components**)
- [ ] tested working for new browsers (Chrome, IE11, IOS) (**"Autocomplete" page's playground will get 'TypeError' using IE 11**) 
- [ ] use ES6 and class syntax 
- [ ] compatible with React 0.14 (seems so)
- [ ] actively updated and supported 
- [ ] should not have major bug reported in GitHub issues
- [ ] open source


<a name="grommet"></a>
### Grommet
- [Grommet](http://www.grommet.io/docs/develop/get-started) 
- [GitHub](https://github.com/grommet/grommet) 
- 188 stars, 24 contributors

- Basics: 
    + [X] dropdownlist / select
    + [X] date picker
    + [ ] time picker
    + [X] tab
    + [X] slide in menu
    + [X] dialog / modal / popup window
    + [X] dropdown menu
    + [X] table
    + [X] responsive
- Extra:
    + [X] loading indicator
    + [ ] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [X] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [ ] theme 
- [ ] tested working for new browsers (Chrome, IE11, IOS) ([**"tab" is not working in Chrome**](http://www.grommet.io/docs/develop/tabs))
- [ ] use ES6 and class syntax 
- [X] compatible with React 0.14
- [ ] actively updated and supported (**lots of issues with no response**)
- [ ] should not have major bug reported in GitHub issues ()
- [X] open source

Not recommend, although it is actively updated, it seems that it lacks support and has bugs.

<a name="elemental-ui"></a>
### Elemental UI

- [Elemental UI](http://elemental-ui.com/home) 
- [GitHub](https://github.com/elementalui/elemental) 
- 1755 stars, 16 contributors

- Basics: 
    + [X] dropdownlist / select
    + [ ] date picker
    + [ ] time picker
    + [ ] tab
    + [ ] slide in menu
    + [X] dialog / modal / popup window
    + [ ] dropdown menu
    + [X] table
    + [X] responsive
- Extra:
    + [X] loading indicator
    + [ ] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [ ] theme 
(**the following is not tested due to too few components**)
- [ ] tested working for new browsers (Chrome, IE11, IOS) 
- [ ] use ES6 and class syntax 
- [ ] compatible with React 0.14
- [ ] actively updated and supported (**Latest commit 27 days ago**)
- [ ] should not have major bug reported in GitHub issues ()
- [ ] open source

This framework has a bootstrap-like look, but it contains too few components.

<a name="belle"></a>
### Belle

- [Belle](http://nikgraf.github.io/belle/#/component/combo-box) 
- [GitHub](https://github.com/nikgraf/belle/) 
- 1060 stars, 12 contributors

- Basics: 
    + [X] dropdownlist / select
    + [X] date picker
    + [ ] time picker
    + [ ] tab
    + [ ] slide in menu
    + [ ] dialog / modal / popup window
    + [ ] dropdown menu
    + [ ] table
    + [ ] responsive (not sure)
- Extra:
    + [ ] loading indicator
    + [X] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [X] theme 
(**the following is not tested due to too few components**)
- [ ] tested working for new browsers (Chrome, IE11, IOS) 
- [ ] use ES6 and class syntax 
- [ ] compatible with React 0.14
- [ ] actively updated and supported 
- [ ] should not have major bug reported in GitHub issues ()
- [ ] open source

This framework has a nice flat material-like look, but it contains too few components.

<a name="react-components-by-khan-academy"></a>
### React Components by Khan Academy

- [React Components by Khan Academy](http://khan.github.io/react-components/) 
- [GitHub](https://github.com/Khan/react-components) 
- 574 stars, 17 contributors

- Basics: 
    + [X] dropdownlist / select
    + [ ] date picker
    + [ ] time picker
    + [ ] tab
    + [ ] slide in menu
    + [X] dialog / modal / popup window
    + [ ] dropdown menu
    + [ ] table
    + [ ] responsive (not sure)
- Extra:
    + [ ] loading indicator
    + [ ] dropdownlist / select with search/filter function (autocomplete)
    + [ ] multi-select
    + [ ] chart
    + [ ] table with sorting, filtering
    + [ ] gridster layout
    + [ ] theme 
(**the following is not tested due to too few components**)
- [ ] tested working for new browsers (Chrome, IE11, IOS) 
- [ ] use ES6 and class syntax 
- [ ] compatible with React 0.14
- [ ] actively updated and supported 
- [ ] should not have major bug reported in GitHub issues ()
- [ ] open source

The development seems very organized and professional. But it contains too few components. Some of them are mixins.

NOTE: It contains:

- drag and drop
- Sortable

## Conclusion
There are many more frameworks like [Semantic UI](http://semantic-ui.com/) which are more focused on CSS, but they needs wrapping is the component needs JS. It turns out clearly after the compare: [Material UI](#material-ui) and [React toolbox](#react-toolbox) are the ones that are ahead.

[Ant Design by Ant Financial (Alibaba)](http://ant.design/docs/introduce), [GitHub](https://github.com/ant-design/ant-design), 1549 stars, 36 contributors
This framework gets lots of attention in China because of the team's technical background.



