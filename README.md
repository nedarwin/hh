# hh
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.ViewHolder> {
    private List<String> myObjects;

    public MyAdapter(List<String> myObjects) {
        this.myObjects = myObjects;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.list_item, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
        String myObject = myObjects.get(position);
        holder.textView.setText(myObject);
    }

    @Override
    public int getItemCount() {
        return myObjects.size();
    }

    public static class ViewHolder extends RecyclerView.ViewHolder {
        public TextView textView;

        public ViewHolder(View itemView) {
            super(itemView);
            textView = itemView.findViewById(R.id.text_view);
        }
    }
}
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Получить список объектов, которые нужно отобразить
        List<String> myObjects = Arrays.asList("f", "f", "f", "f", "f");

        // Создать адаптер и передать список объектов
        MyAdapter adapter = new MyAdapter(myObjects);

        // Найти RecyclerView в макете и установить адаптер и LayoutManager
        RecyclerView recyclerView = findViewById(R.id.rc);
        recyclerView.setAdapter(adapter);
        recyclerView.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.HORIZONTAL, false));
    }
}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="8dp">

    <ImageView
        android:id="@+id/image_view"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:scaleType="centerCrop" />

    <TextView
        android:id="@+id/text_view"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:gravity="center_horizontal"
        android:textSize="16sp" />

</LinearLayout>
