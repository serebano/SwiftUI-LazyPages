# Changelog

All notable changes to SwiftUI-LazyPages will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-09-24

### Added
- 🚀 **Performant GoTo Page**: Instant navigation to any page without loading intermediate pages
- 🎯 **Flicker-Free Navigation**: Eliminated page flickering during programmatic jumps
- ⚡ **Large Dataset Support**: Optimized for 100,000+ items with constant memory usage
- 🔄 **Improved View Recycling**: Better view lifecycle management during large jumps
- 📱 **Production Ready**: Stable, tested implementation

### Changed
- **BREAKING**: Forked from original SwiftUI-LazyPager for performance optimizations
- **Enhanced**: `goToPage` method completely rewritten for performance
- **Optimized**: View loading strategy for large jumps
- **Improved**: Scroll delegate handling during programmatic navigation

### Technical Details
- Modified `PagerView.goToPage()` to clear intermediate views on large jumps
- Added `isProgrammaticNavigation` flag to prevent scroll delegate interference  
- Ensured `currentIndex` is set before `computeViewState()` for proper view alignment
- Implemented temporary delegate disabling during navigation to prevent settling issues

### Performance Improvements
- **Navigation Speed**: Large jumps now happen instantly regardless of distance
- **Memory Usage**: Constant memory footprint regardless of dataset size or jump distance
- **UI Stability**: No more flickering or incorrect page display during navigation
- **Responsiveness**: Immediate user feedback for all navigation actions

## [0.x.x] - Previous Versions
- Based on original SwiftUI-LazyPager by Brian Floersch
- Basic paging functionality with performance limitations for large datasets
