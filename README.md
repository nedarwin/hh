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

// Создаем объект Gson
Gson gson = new Gson();

// Создаем объект, представляющий тело запроса
OrderRequest orderRequest = new OrderRequest();

// Заполняем поля объекта orderRequest
orderRequest.address = "string";
orderRequest.date_time = "string";
orderRequest.phone = "string";
orderRequest.comment = "string";
orderRequest.audio_comment = "string";

Patient patient = new Patient();
patient.name = "string";

Item item = new Item();
item.catalog_id = 1;
item.price = "string";
patient.items = new ArrayList<>();
patient.items.add(item);

orderRequest.patients = new ArrayList<>();
orderRequest.patients.add(patient);

// Преобразуем объект orderRequest в JSON-строку с помощью Gson
String json = gson.toJson(orderRequest);

// Создаем экземпляр OkHttp клиента
OkHttpClient client = new OkHttpClient();

// Создаем тело запроса в формате JSON с помощью json строки
RequestBody body = RequestBody.create(MediaType.parse("application/json"), json);

// Создаем объект Request
Request request = new Request.Builder()
        .url("https://medic.madskill.ru/api/order")
        .post(body)
        .addHeader("accept", "application/json")
        .addHeader("Content-Type", "application/json")
        .build();

// Отправляем запрос
try {
    Response response = client.newCall(request).execute();
    // Обрабатываем ответ
} catch (IOException e) {
    e.printStackTrace();
}
