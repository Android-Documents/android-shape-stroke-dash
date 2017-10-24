# android-shape-stroke-dash
Android 关于shape画虚线

## 解决问题：
View中添加Drawable中shape，显示的是实线。

## 实现虚线的shape画法：shape_dash_line.xml

```
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="line">

    <stroke
        android:width="1dp"
        android:color="@color/color_e5e5e5"
        android:dashGap="3dp"
        android:dashWidth="4dp" />
    <size android:height="0.5dp" />
</shape>
```

## 然后在view中添加background为@drawable/shape_dash_line,

```
<View
            android:layout_width="match_parent"
            android:layout_height="2dp"
            android:layout_marginBottom="@dimen/margin_15"
            android:layout_marginTop="@dimen/margin_12"
            android:background="@drawable/shape_dash_line"
            android:layerType="software"
            android:paddingEnd="@dimen/padding_18"
            android:paddingStart="@dimen/padding_18" />
```

### 问题1：画的虚线为什么没有显示出来？

解答：原因在于设置的 view 的高度与 shape 虚线的高度相同。因此不会显示，只需要将 view 中的 layout_height 设置的比 shape 虚线的高度大就可以。例如：将 layout_height=“1dp” 改为 layout_height=“1.5dp” 。

### 问题2：本该显示的虚线，为什么显示为实线？

解答：原因在于 Android 3.0 之后，系统默认关闭了硬件加速功能。所以你可以使用以下方法。

```
view.setLayerType(View.LAYER_TYPE_SOFTWARE, null);
在AndroidManifest文件中，在需要用到虚线的activity的添加属性

<activity android:hardwareAccelerated="false" />
```
