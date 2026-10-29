# settings_row_filter.py

    #!/usr/bin/env python3
    """Filter a laser settings CSV to one machine, material and thickness.

    A settings row is only valid for the material and thickness its maker
    printed. Copy rows with their columns, never by wattage alone.
    """
    import csv, sys

    def rows_for(path, machine, material, thickness_mm):
        with open(path, newline="") as fh:
            for row in csv.DictReader(fh):
                if (row.get("machine") == machine
                        and row.get("material") == material
                        and float(row.get("thickness_mm", "nan")) == thickness_mm):
                    yield row

    if __name__ == "__main__":
        path, machine, material, thickness = sys.argv[1:5]
        for row in rows_for(path, machine, material, float(thickness)):
            print(row)


Filter laser settings CSV rows by machine, material and thickness : a settings row is only valid for the material and thickness its maker printed. Safety statements about paper are quoted from the makers with their documented conditions on CutChart's [paper safety page](https://cutchart.com/safety/paper/).

MIT License. This utility is original tooling and makes no safety claim.
