An _intent_ is an object that a _component_ can use to communicate with the OS. _component_ in android are activities, services, broadcast receivers and content providers.
```java
mCheatButton = (Button) findViewById(R.id.cheat_button);
mCheatButton.setOnClickListener (new View.OnClickListener() {
    @override
    public void onClick(View v) {
        Intent intent = new Intent(QuizActivity.this, CheatActivity.class)
        startActivity(intent)
    }    
}
```
with Kotlin Android Extensions
```kotlin
val cheatButton.setOnClickListener {
    val intent = Intent(QuizActivity.this, CheatActivity.class)
    startActivity(intent)
}
```
