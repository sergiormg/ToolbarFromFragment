# ToolbarFromFragment
[![Build Status](https://travis-ci.org/sergiormg/ToolbarFromFragment.svg?branch=master)](https://travis-ci.org/sergiormg/ToolbarFromFragment)

Using toolbars within fragments.

Imagine you have an application that uses the navigation drawer and each fragment has their own toolbar. When you change fragment the toolbar will change accordingly:

```xml
<android.support.v7.widget.Toolbar
    android:id="@+id/toolbar"
    app:title="@string/first_fragment"
    android:layout_width="match_parent"
    android:layout_height="?attr/actionBarSize"
    android:background="?attr/colorPrimary"
    app:popupTheme="@style/AppTheme.PopupOverlay" />
```

To do that, first you need to set the new toolbar in your fragment during `onCreateView`:
```java
((AppCompatActivity) getActivity()).setSupportActionBar((Toolbar) view.findViewById(R.id.toolbar));
```

And then, in your activity, you need to execute some code to make sure that your toolbar deal with the navigation drawer:
```java
// Restores the behaviour of action bar and ActionBarDrawerToggle
ActionBar actionBar = getSupportActionBar();
if (actionBar != null) {
    actionBar.setDisplayHomeAsUpEnabled(true);
    actionBar.setHomeButtonEnabled(true);
}

mDrawerToggle = new ActionBarDrawerToggle(
        this,
        mDrawerLayout,
        R.string.navigation_drawer_open,
        R.string.navigation_drawer_close
) {
    @Override
    public void onDrawerOpened(View drawerView) {
        super.onDrawerOpened(drawerView);
    }
};

// Synchronizes the state of the drawer indicator with the DrawerLayout
mDrawerLayout.post(new Runnable() {
    @Override
    public void run() {
        mDrawerToggle.syncState();
    }
});

mDrawerLayout.addDrawerListener(mDrawerToggle);
```


Check out the full example to test how it works!
