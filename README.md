# SpannableString使用记录

[![](https://jitpack.io/v/ALguojian/SpannableHelper.svg)](https://jitpack.io/#ALguojian/SpannableHelper)

<div align=center><img width="350" height="600" src="http://ouvjn19yd.bkt.clouddn.com/TIM%E5%9B%BE%E7%89%8720171104002659.png"/></div>

1.Add it in your root build.gradle at the end of repositories:
```
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```
2.Add the dependency
```
	dependencies {
	        compile 'com.github.ALguojian:SpannableHelper:1.0'
	}

```


用法：
```
  SpannableStringUtils spannableStringUtils = new SpannableStringUtils("飞流直下三千尺，疑是银河落九天");

          spannableStringUtils.setColor(Color.GREEN, 2, 6)
                  .setBackGround(ContextCompat.getColor(this,R.color.bbb), 4, 8)
                  .setBold(6, 10)
                  .setOnClick(9, 14, ContextCompat.getColor(this,R.color.aaa))
                  .setImage(this, R.mipmap.ic_launcher, 3, 6, 120, 160)
                  .setOnClickSpanListener(new SpannableStringUtils.OnClickSpanListener() {
                      @Override
                      public void OnClickSpanListener() {

                          Toast.makeText(MainActivity.this, "点我", Toast.LENGTH_SHORT).show();
                      }
                  });

          textView.setMovementMethod(LinkMovementMethod.getInstance());
          textView.setTextSize(20);
          textView.setText(spannableStringUtils);

```

### 简介：
`spannableString`和`string`类似都是一种字符串类型，都可以用于`textview`设置为版本

`setSpan((Object what, int start, int end, int flags))`

- `what`:设置格式
- `start`：开始下标索引
- `end`：结束下表索引
- `flags`：
    - `Spanned.SPAN_INCLUSIVE_EXCLUSIVE`从起始下标到终了下标，包括起始下标
    - `Spanned.SPAN_INCLUSIVE_INCLUSIVE` 从起始下标到终了下标，同时包括起始下标和终了下标
    - `Spanned.SPAN_EXCLUSIVE_EXCLUSIVE` 从起始下标到终了下标，但都不包括起始下标和终了下标
    - `Spanned.SPAN_EXCLUSIVE_INCLUSIVE` 从起始下标到终了下标，包括终了下标


#### 设置监听事件
```
 SpannableString spannableString = new SpannableString(item.getContent());

    ClickableSpan span = new ClickableSpan() {

        @Override
        public void onClick(View widget) {

            ToastUtils.show(getActivity(), "haha");

        }

        @Override
        public void updateDrawState(TextPaint ds) {
            super.updateDrawState(ds);
            ds.setColor(ds.linkColor);
            ds.setUnderlineText(false);
       }
    };
spannableString.setSpan(span, 2, item.getContent().length(), Spannable.SPAN_EXCLUSIVE_INCLUSIVE);
ForegroundColorSpan cspan = newForegroundColorSpan(Color.parseColor("#57caa1"));
spannableString.setSpan(cspan, 2, item.getContent().length(), Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
TextView textView = helper.getView(R.id.group_count);
textView.setText(spannableString);
//控制点击的时候的背景色
textView.setHighlightColor(Color.parseColor("#57caa1"));
textView.setMovementMethod(LinkMovementMethod.getInstance());
```




