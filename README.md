# UITextView-Text-RealityKit-SwiftUI
UITextView Text RealityKit SwiftUI
# The first part
![IMG_0269](https://github.com/S-way520/UITextView-Text-RealityKit-SwiftUI/assets/95877651/5347cc10-0988-4369-bd82-4ff8a3a202c6)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
struct ContentView: View {
    @State private var text = UserDefaults.standard.string(forKey: "TextViewText") ?? ""
    func saveText() { UserDefaults.standard.set(text, forKey: "TextViewText") }
    var body: some View {
        TextView(text: $text)
        Button("保存") {
            saveText()
        }.padding(30)
    }
}
struct TextView: UIViewRepresentable {
    @Binding var text: String
    let textView = UITextView()
    func makeUIView(context: Context) -> UITextView {
        textView.delegate = context.coordinator
        textView.font = UIFont.systemFont(ofSize: 24)
        textView.isScrollEnabled = true
        textView.isEditable = true
        return textView
    }
    func updateUIView(_ uiView: UITextView, context: Context) {
        uiView.text = text
    }
    func makeCoordinator() -> Coordinator {
        Coordinator(self)
    }
    class Coordinator: NSObject, UITextViewDelegate {
        let parent: TextView
        init(_ parent: TextView) {
            self.parent = parent
        }
        func textViewDidChange(_ textView: UITextView) {
            parent.text = textView.text
        }
    }
}
```
