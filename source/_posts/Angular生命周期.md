---
title: Angular生命周期
date: 2023-01-05 16:25:52
tags: Angular
---

## 生命周期的顺序

### ngOnChanges

如果组件绑定过输入属性，那么在 ngOnInit() 之前以及所绑定的一个或多个输入属性的值发生变化时都会调用。

### ngOnInit

在第一轮 ngOnChanges() 完成之后调用，只调用一次。而且即使没有调用过 ngOnChanges()，也仍然会调用 ngOnInit()（比如当模板中没有绑定任何输入属性时）。

### ngDoCheck

紧跟在每次执行变更检测时的 ngOnChanges() 和 首次执行变更检测时的 ngOnInit() 后调用。

### ngAfterContentChecked

ngAfterContentInit() 和每次 ngDoCheck() 之后调用。

### ngAfterViewInit

第一次 ngAfterContentChecked() 之后调用，只调用一次。

### ngAfterViewChecked

ngAfterViewInit() 和每次 ngAfterContentChecked() 之后调用。

### ngOnDestroy

在 Angular 销毁指令或组件之前立即调用。
