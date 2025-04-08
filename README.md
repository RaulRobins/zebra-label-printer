# Zebra Label Printer Python Script

![Zebra Printer](https://img.shields.io/badge/Zebra-Printer-blue) ![Python](https://img.shields.io/badge/Python-3.7%2B-green) ![License](https://img.shields.io/badge/License-MIT-orange)

A Python package for generating and printing labels to Zebra printers using ZPL (Zebra Programming Language).

## Features

- 🖨️ Print to Zebra printers (network, USB, or serial)
- 📝 Manage ZPL templates with variable substitution
- ⌨️ Command line interface for easy integration
- 📊 Support for barcodes, text, boxes, and graphics
- 🔄 Multiple connection types (TCP/IP, USB, serial)
- 🏷️ Pre-designed label templates included
- 🧪 Unit tested core functionality

## Installation

### Prerequisites

- Python 3.7+
- Zebra printer with network/USB connection
- (Optional) Virtual environment

### Install from source

```bash
git clone https://github.com/yourusername/zebra-label-printer.git
cd zebra-label-printer
pip install -r requirements.txt
```

### Install as package

```bash
pip install git+https://github.com/yourusername/zebra-label-printer.git
```

## Usage

### Python API

```python
from zebra_label_printer import ZebraPrinter

# Initialize printer
printer = ZebraPrinter(ip_address="192.168.1.100", port=9100)

# Print simple label
printer.print_label(
    template="shipping_label",
    data={
        "title": "FRAGILE",
        "barcode": "123456789",
        "content": "Handle with care"
    }
)
```

### Command Line Interface

```bash
python -m zebra_label_printer.cli \
    --template shipping_label \
    --data '{"title":"FRAGILE","barcode":"12345"}' \
    --printer 192.168.1.100
```

### Available Templates

1. `shipping_label` - Standard shipping label with barcode
2. `product_label` - Product identification label
3. `barcode_only` - Simple barcode label
4. `address_label` - Mailing address label

## Template Customization

Create your own ZPL templates in the `templates/` directory. Use `{variable_name}` for dynamic content.

Example template (`templates/product_label.zpl`):

```zpl
^XA
^FO20,20^A0N,40^FDProduct: {product_name}^FS
^FO20,70^BY2^BCN,100,Y,N,N^FD{barcode}^FS
^FO20,180^A0N,30^FDPrice: ${price}^FS
^XZ
```

## Configuration

Create a `config.ini` file to store default printer settings:

```ini
[printer]
default_ip = 192.168.1.100
port = 9100
default_template = shipping_label
timeout = 5
```

## Troubleshooting

**Common Issues:**

| Problem                | Solution                                          |
| ---------------------- | ------------------------------------------------- |
| Printer not responding | Check network connection and port (default: 9100) |
| Incorrect label format | Verify your ZPL template syntax                   |
| Variables not replaced | Ensure template uses {curly_braces} for variables |
| Partial prints         | Check label dimensions match physical label size  |

## Development

### Running Tests

```bash
python -m pytest tests/
```

### Building the Package

```bash
python setup.py sdist bdist_wheel
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

Your Name - [@yourtwitter](https://twitter.com/yourtwitter) - your.email@example.com

Project Link: [https://github.com/yourusername/zebra-label-printer](https://github.com/yourusername/zebra-label-printer)

---

**References:**

- [ZPL Programming Guide](https://www.zebra.com/content/dam/zebra/manuals/printers/common/programming/zpl-zbi2-pm-en.pdf)
- [PyZPL Documentation](https://pyzpl.readthedocs.io/)
