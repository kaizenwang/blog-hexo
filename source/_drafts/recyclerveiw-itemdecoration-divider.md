---
date: 2016-09-20 16:56:17
title: RecyclerVeiw ItemDecoration add divider
---

使用RecyclerView的时候不能直接添加divider用于分割每个item

不过可以使用`addItemDecoration`来实现divider的效果

```java
mRecyclerView.addItemDecoration(new RecyclerView.ItemDecoration() {

      @Override
      public void onDraw(Canvas c, RecyclerView parent, RecyclerView.State state) {
        Drawable drawable = new ColorDrawable(Color.BLACK);
        final int left = parent.getPaddingLeft();
        final int right = parent.getWidth() - parent.getPaddingRight();
        final int childCount = parent.getChildCount();
        for (int i = 0; i < childCount; i++) {
          final View child = parent.getChildAt(i);
          final RecyclerView.LayoutParams layoutParams =
              (RecyclerView.LayoutParams) child.getLayoutParams();
          final int top = child.getBottom() + layoutParams.bottomMargin +
              Math.round(ViewCompat.getTranslationY(child));
          final int bottom = top + 1;
          drawable.setBounds(left, top, right, bottom);
          drawable.draw(c);
        }
      }

      @Override
      public void getItemOffsets(Rect outRect, View view, 
                                 RecyclerView parent, 
                                 RecyclerView.State state) {
        outRect.set(0, 0, 0, 1);
      }
    });
```



