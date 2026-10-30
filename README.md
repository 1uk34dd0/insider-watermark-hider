# Insider Watermark Hider

A [Windhawk](https://windhawk.net/) mod that hides the build watermark Windows Insider builds draw in the bottom-right corner of the desktop:

> Windows 11 Pro Insider Preview
> Evaluation copy. Build XXXXX.XXXX

<!-- Add a before/after screenshot here, e.g. ![Before and after](docs/before-after.png) -->

## Features

- Hides the "Evaluation copy / Insider Preview" desktop watermark
- No system files or registry settings are modified
- Fully reversible: disable the mod and the watermark returns
- Narrow text matching, so normal Explorer text (such as file names) is left alone

## Requirements

- Windows 11 running an Insider Preview build
- [Windhawk](https://windhawk.net/) installed

## Installation

### From the Windhawk catalogue

1. Open Windhawk and go to **Explore**.
2. Search for **Insider Watermark Hider**.
3. Click **Install**.

### Manually

1. Open Windhawk and choose **Create a new mod**.
2. Replace the template with the contents of [`insider-watermark-hider.wh.cpp`](insider-watermark-hider.wh.cpp).
3. Compile the mod and make sure it is enabled.

If the watermark is still visible afterwards, restart Windows Explorer so the desktop repaints: open Task Manager, find **Windows Explorer**, and choose **Restart**.

## How it works

The mod runs inside `explorer.exe` and hooks the text-drawing functions the desktop uses:

- `DrawTextW`
- `DrawTextExW`
- `ExtTextOutW`
- `TextOutW`
- `DrawThemeTextEx`

If the text being drawn contains "Evaluation copy" or "Insider Preview", the call is skipped, so the watermark is never painted.

## Limitations

- This only hides the watermark visually. It does not change the build, its licensing, or its pre-release status.
- Microsoft may change how the watermark is drawn in a future Insider build, which could stop the mod from working. Please open an issue if that happens.
- The mod is only tested on the builds listed below. Other builds may work but are unverified.

| Windows build | Status |
| ------------- | ------ |
| `<<< YOUR BUILD NUMBER >>>` | Working |

## Troubleshooting

**The watermark is still showing**

1. Check the mod is enabled in Windhawk.
2. Restart Windows Explorer (see above).
3. If it still appears, set `VERBOSE` to `1` near the top of the source, recompile, and restart Explorer. The Windhawk log output will list text containing "Build" or "Windows" and the function that drew it. Open an issue and include the log lines, your Windows build number, and your Windhawk version.

**Explorer behaves strangely**

Disable the mod in Windhawk. Windhawk can be less stable on Insider builds, so it is worth checking whether the problem also happens with other mods disabled.

## Contributing

Issues and pull requests are welcome. If you are reporting a bug, please include your Windows build number and the log output described above.

## Disclaimer

This project is not affiliated with or endorsed by Microsoft. Windhawk is developed separately by [Ramen Software](https://ramensoftware.com/windhawk). Use at your own risk.

## License

[MIT](LICENSE)
