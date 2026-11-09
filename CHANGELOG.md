# Changelog

## Unreleased

### Added
- Plugin data API in `ReCoPa.Plugins`: `DataPacket`, `DataQuery`, `IDataAccess`, `IDataStore`, `IDataConsumer` and `IDataAccessConsumer`. Plugin components can receive live socket events and query a rolling store of recent events.
- `DataHub` in the host keeps the last 10,000 received events and passes them to every plugin component that implements `IDataConsumer` or `IDataAccessConsumer`.
- The xAPI plugins Activity Pulse, Focus Distribution, Task State and xAPI Preview show live statements (`XApiStatementParser`).
- `ReCoPa.Plugins/README.md`: guide for writing plugins.
- Architecture decision records in `docs/adr/` (0001-0008).
- The `hello` frame is parsed into `ClientHello` (session ID, headers, meta) and raised as `SocketServerHost.ClientHello`. The connection keeps the client's session ID in `ClientSessionId`.
- The sidebar button starts and stops the eye calibration (`calibration:start`, `calibration:stop`) and shows its state from `isCalibrating`.

### Changed
- Session tabs are named after the client's session ID instead of its endpoint. Connect and disconnect toasts show the session ID.
- Closing a session tab saves the session and marks it as closed, so it is not restored at the next start.
- The eye calibration controls follow `isCalibratable` from the tracking metadata. `isCalibrated` is still read when `isCalibratable` is missing.

### Fixed
- The dashboard shows the empty state when no session view is selected, instead of an empty area.

## ReCoPa v0.0.1 (2026-02-05)

### Summary
ReCoPa v2 is a cross-platform researcher companion panel for real-time data capture, visualization, and analysis of XR learning sessions. This release focuses on a modular plugin system, live visual analytics, and xAPI/LRS integration, built on Avalonia and ReactiveUI.

### Highlights
- Cross-platform desktop UI (Windows, macOS, Linux) via Avalonia
- Extensible plugin architecture with runtime component loading
- Live visualizations with LiveCharts + SkiaSharp
- Built-in xAPI integration with Learning Record Store support
- Reactive architecture optimized for real-time data streams

### New Features
- Plugin System v2
- Plugin packages with metadata, contributors, and multiple component types
- Interfaces for visualization, data sources, endpoints, and filters
- Auto-loading plugins from platform-specific directories
- Socket Server for Real-Time Data
- Custom binary protocol for high-throughput XR session streams
- UI-safe dispatching for real-time updates
- Live Analytics Dashboards
- Dedicated views for sessions, statements, clients, and visualizations
- Charting stack tuned for performance
- xAPI Plugin Bundle
- Example visualizations: Activity Pulse, Focus Distribution, Task State, xAPI Preview
- LRS connectivity out of the box

### Improvements
- Centralized dependency management via Directory.Packages.props
- Nullable reference types enabled across the solution
- Compiled Avalonia bindings for performance and compile-time safety
- ReactiveUI-based MVVM throughout the UI layer
- SukiUI theming and toast notifications for modern UX

### Developer Notes
- Start the desktop client with dotnet run --project ReCoPa.Desktop
- Hot reload supported via dotnet watch
- Socket server defaults to port 4567
- Plugins auto-load from standard OS directories

### Known Limitations (Research Prototype)
- No plugin marketplace or automatic updates yet
- Session playback and recording not implemented
- Advanced filtering UI is pending
- Cloud sync not available

### Upgrade / Compatibility
- Requires .NET 10.0 or later
- Works on macOS, Windows, and Linux
- Existing plugins must implement new interfaces from ReCoPa.Plugins

### Acknowledgments
Built with Avalonia, ReactiveUI, LiveCharts, and SukiUI.
Lead Developer: Sergej Görzen
