---
layout:		post
comments:	true
title:		"Google Mock array matcher"
date:		2015-07-26
categories:
- cpp
- gmock
---

Just in case somebody is also stuck with the following compiler error while using GMock ElementsAreArray matcher:

> error: 'testing::internal::StlContainerView<int*>::type {aka int*}' is not a class, struct, or union type ::std::vector<Matcher<const Element&> > matchers_;

For example, we have the following interface:

{% highlight cpp %}
class ArrayInterface
{
public:
    virtual void update(int size, int *arr) = 0;
};
{% endhighlight %}

*NOTE*: the order here is different, when usual. Usually pointer to array goes first, and then size, and this is what `ElementsAreArray` matcher expects.

Because of changed order, we have to tell GMock how to map values from the mocked function to the matcher, which can be done using `With(Args<>())` construction:

{% highlight cpp %}
EXPECT_CALL(mock, update(_, _)).With(Args<1, 0>(ElementsAreArray({1, 2})));
{% endhighlight %}

`Args` allows us to manipulate function arguments in tuple like fashion, there value `0` stands for a first function argument.