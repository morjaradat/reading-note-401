# Create dynamic lists with RecyclerView

- we use recyclerView for display a large data .
- When an item scrolls off the screen, RecyclerView doesn't destroy its view. Instead, RecyclerView reuses the view for new items that have scrolled onscreen.

***how to build a dynamic list :***

- RecyclerView is the ViewGroup that contains the views corresponding to your data.
- Each individual element in the list is defined by a view holder object
- The RecyclerView requests those views, and binds the views to their data, by calling methods in the adapter.
- The layout manager arranges the individual elements in your list.

***Steps for implementing your RecyclerView***

1. decide how the style look.
2. Design how each element in the list is going to look and behave.
3. Define the Adapter that associates your data with the ViewHolder views.

***Plan your layout***

- The items in your RecyclerView are arranged by a LayoutManager class.
- The RecyclerView library provides three layout managers :

1. LinearLayoutManager arranges the items in a one-dimensional list.
2. GridLayoutManager arranges all items in a two-dimensional grid:
   -If the grid is arranged vertically, GridLayoutManager tries to make all the elements in each row have the same width and height, but different rows can have different heights.
   -If the grid is arranged horizontally, GridLayoutManager tries to make all the elements in each column have the same width and height, but different columns can have different widths.

3. StaggeredGridLayoutManager is similar to GridLayoutManager, but it does not require that items in a row have the same height or same width .

***Implementing your adapter and view holder***

- we need to implement your Adapter and ViewHolder .
- These two classes work together to define how your data is displayed.
- The ViewHolder is a wrapper around a View that contains the layout for an individual item in the list.
- The Adapter creates ViewHolder objects as needed, and also sets the data for those views.

***after implement the adapter***

- we need to overriding three methods :

1. onCreateViewHolder() : recyclerView will call this method to create new ViewHandler .

2. onBindViewHolder() : RecyclerView calls this method to associate a ViewHolder with data.

3. getItemCount() :RecyclerView calls this method to get the size of the data set.

