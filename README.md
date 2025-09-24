# SwiftUI-LazyPages

A performant, lazy-loaded paging view for SwiftUI that handles large datasets efficiently.

## ✨ Features

- **🚀 Performant GoTo Page**: Jump to any page instantly without loading intermediate pages
- **🎯 No Flickering**: Stable page positioning without drift or settling issues  
- **⚡ Instant Navigation**: Handle 100,000+ items with instant jumps
- **🔄 Lazy Loading**: Only loads visible pages plus a configurable preload amount
- **📱 Full Platform Support**: iOS, iPadOS, macOS, watchOS, tvOS, visionOS
- **🎨 Customizable**: Direction, spacing, zoom, dismiss gestures, and more

## 🛠 Installation

### Swift Package Manager

Add this to your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/serebano/SwiftUI-LazyPages", from: "1.0.0")
]
```

Or add it through Xcode: File → Add Package Dependencies → `https://github.com/serebano/SwiftUI-LazyPages`

## 📖 Basic Usage

```swift
import SwiftUI
import LazyPager

struct ContentView: View {
    @State private var currentPage = 0
    let data = Array(0..<100000) // Large dataset
    
    var body: some View {
        VStack {
            Text("Page \(currentPage + 1) of \(data.count)")
            
            Button("Jump to 50,000") {
                currentPage = 49999 // Instant jump!
            }
            
            LazyPager(data: data, page: $currentPage) { index in
                Text("Page \(index + 1)")
                    .frame(maxWidth: .infinity, maxHeight: .infinity)
                    .background(Color.blue.opacity(0.1))
            }
        }
    }
}
```

## 🎯 Advanced Usage

### Custom Data Types

```swift
struct ContentView: View {
    @State private var currentPage = 0
    let items: [MyItem]
    
    var body: some View {
        LazyPager(data: items, page: $currentPage) { item in
            MyCustomView(item: item)
        }
        .shouldLoadMore { 
            loadMoreItems() 
        }
        .pageSpacing(16)
        .onTap { 
            handleTap() 
        }
    }
}
```

### Vertical Paging

```swift
LazyPager(data: data, page: $currentPage, direction: .vertical) { item in
    ItemView(item: item)
}
```

### With Zoom Support

```swift
LazyPager(data: images, page: $currentPage) { image in
    Image(image.name)
        .resizable()
        .aspectRatio(contentMode: .fit)
}
.zoomable(min: 1.0, max: 4.0)
```

## ⚡ Performance Optimizations

This fork includes significant performance improvements:

### Large Dataset Navigation
- **Before**: Jumping from page 1 to page 50,000 would load all 49,999 intermediate pages
- **After**: Instantly jumps to page 50,000 without loading intermediate pages

### Flicker-Free Navigation
- **Before**: Pages would briefly show incorrect content then "settle" to the right page
- **After**: Pages display exactly the right content immediately

### Memory Efficient
- Only keeps a small window of pages in memory (configurable via `preloadAmount`)
- Automatically cleans up distant pages to prevent memory bloat

## 🔧 Configuration

```swift
LazyPager(data: data, page: $currentPage) { item in
    ItemView(item: item)
}
.settings { config in
    config.preloadAmount = 5      // Pages to keep in memory
    config.pageSpacing = 20       // Space between pages
    config.dismissVelocity = 1.5  // Swipe sensitivity
}
```

## 🎨 Customization Options

- **Direction**: `.horizontal` or `.vertical`
- **Page Spacing**: Custom spacing between pages
- **Zoom**: Pinch-to-zoom with configurable min/max scales
- **Dismiss Gesture**: Swipe-to-dismiss with custom callbacks
- **Load More**: Pagination support for infinite scrolling
- **Overscroll**: Custom handling for end-of-content

## 📱 Platform Support

- iOS 13.0+
- iPadOS 13.0+  
- macOS 10.15+
- watchOS 6.0+
- tvOS 13.0+
- visionOS 1.0+

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

Based on the original [SwiftUI-LazyPager](https://github.com/gh123man/SwiftUI-LazyPager) by Brian Floersch, enhanced with performance optimizations for large datasets.

## 📊 Performance Comparison

| Feature | Original LazyPager | SwiftUI-LazyPages |
|---------|-------------------|-------------------|
| Large jumps (1→50k) | Loads 49,999 pages | Instant jump |
| Page flickering | Yes | No |
| Memory usage | Grows with jumps | Constant |
| Navigation speed | Slow for large jumps | Always instant |

## 🚀 Migration from Original

SwiftUI-LazyPages is a drop-in replacement. Simply change your import:

```swift
// Before
import SwiftUILazyPager

// After  
import LazyPager
```

All existing APIs remain the same, with added performance benefits automatically applied.
