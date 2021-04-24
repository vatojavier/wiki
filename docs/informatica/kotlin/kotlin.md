# Kotlin

## Databinding
Te permite acceder a todos los recursos del layout sin tener que hacer findViewById()

1. Activar DataBinding en el build.graddle (app):
```
android{
  ...
  buildFeatures{
        dataBinding = true
   }
}
```

2. Envolver ficher de diseño de actividad/fragmento en un `<layout>`:
```xml
<layout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <LinearLayout
        android:id="@+id/main"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        ...
```

3. Declarar e inicializar el objeto binding:

  - Si es una actividad se inicializa en onCreate():
```kotlin
class MainActivity : AppCompatActivity() {
    lateinit var binding: ActivityMainBinding
    ...
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        binding.generateButton.setOnClickListener {viewModel.generateNumber()}
    }
```

  - Si es un fragmento se hace en OnCreateView():
```kotlin
class MainFragment: Fragment() {
    lateinit var binding: FragmentMainBinding
    
    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {
        binding = DataBindingUtil.inflate<FragmentMainBinding>(
            inflater,
            R.layout.fragment_main,
            container,
            false)

        return binding.root
        // Y ya se puede usar jaujas
    }
```

## Comparar fragments en un FrameLayout
Teniendo `MainFragment` como una clase que hereda de `Fragment()`
```kotlin
var fragment = supportFragmentManager.findFragmentById(R.id.container) // Id del frame que aloja al fragmen

if(fragment is MainFragment){
  // Hacer movidas
}
```
Si no va algo, meter los diseños en un `<layout>` y espabilando.


## RoomDatabse con ViewModel y LiveData
Cuando se hace una query, se hace de forma async por lo que es necesario que esta devuelva un LiveData para que cuando se reciba el resultado se pueda realizar alguna acción (actualizar el UI o asignar otros valores etc).

Ejemplo actualizar valor con query:

viewModel:
```Kotlin
class StatisticsViewModel(application: Application): AndroidViewModel(application) {
    private val context = getApplication<Application>().applicationContext
    
    // Las queries devuelven un LiveData<Int>
    val nEasy = CardDatabase.getInstance(context).cardDao.getNEasyCards()
    val nDoubt = CardDatabase.getInstance(context).cardDao.getNDoubtCards()
    val nHard = CardDatabase.getInstance(context).cardDao.getNHardCards()
}
```

fragmet:
```Kotlin
class StatisticsFragment: Fragment() {

    private val statisticsViewModel: StatisticsViewModel by lazy {
        ViewModelProvider(this).get(StatisticsViewModel::class.java)
    }
    
    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {

        binding = DataBindingUtil.inflate(
            inflater,
            R.layout.fragment_statistics,
            container,
            false
        )
        
        var easy = 0
        var doubt = 0
        var hard = 0

        statisticsViewModel.apply {
            nEasy.observe(
                    viewLifecycleOwner,
                    Observer {
                        easy = it // Es aquí cuando se completa la query y se actualiza el valor
                    }
            )
            nDoubt.observe(
                    viewLifecycleOwner,
                    Observer {
                        doubt = it // Es aquí cuando se completa la query y se actualiza el valor
                    }
            )
            nHard.observe(
                    viewLifecycleOwner,
                    Observer {
                        hard = it // Es aquí cuando se completa la query y se actualiza el valor
                    }
            )
        }
        
        // Aquí, easy, doubt y hard pueden ser 0 u el valor de la query dependiendo de si ha llegao a completarse la query
        
        return binding.root

    }
    
```

