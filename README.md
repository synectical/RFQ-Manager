# rfq-manager

## Local Development Setup

1. **Create a virtual environment:**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the server locally:**
   ```bash
   uvicorn rfq-manager.main:app --reload
   ```

## systemd Service Example

Create a file `/etc/systemd/system/rfq-manager.service` with:

```ini
[Unit]
Description=RFQ Manager FastAPI app
After=network.target

[Service]
User=rfqmanager
Group=rfqmanager
WorkingDirectory=/path/to/your/repo
Environment="PATH=/path/to/your/repo/.venv/bin"
ExecStart=/path/to/your/repo/.venv/bin/uvicorn rfq-manager.main:app --host 0.0.0.0 --port 8000

[Install]
WantedBy=multi-user.target
```

- Replace `/path/to/your/repo` and user/group as needed.
- Reload systemd and start:
  ```bash
  sudo systemctl daemon-reload
  sudo systemctl start rfq-manager
  sudo systemctl enable rfq-manager
  ```

## Docker Usage

Build and run the container:

```bash
docker build -t rfq-manager .
docker run -d -p 8000:8000 rfq-manager
```