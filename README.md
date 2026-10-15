# OptoSense Defect Classification Dataset (synthetic)

**Scenario.** You are the data science team at a plant that assembles optoelectronic components similar to the OPTEK range: IR emitters, phototransistors, slotted optical switches and reflective object sensors. Every unit passes through die attach, wire bonding, moulding, curing and reflow, then an end-of-line electrical test, X-ray and visual inspection, and a short burn-in. Management wants a model that flags defective units and identifies the failure mechanism so the right process team can respond.

All data is synthetic. Part numbers, suppliers, machines and operators are fictional and do not represent real products or performance.

## Files

| File | Rows | Description |
|---|---|---|
| `optek_defects_train.csv` | ~50,100 | Jan 5 – Jun 3, 2026, with labels |
| `optek_defects_test.csv` | ~10,150 | Jun 4 – Jul 3, 2026, labels removed |
| `optek_defects_test_labels.csv` | ~10,150 | Held-out answer key (lecturer only) |
| `generate_optek_defect_dataset.py` | | Regenerates everything; change `--seed` for a different version per cohort |

The split is by time, not random, so the test set reflects deployment on future production.

## Data dictionary

| Column | Type | Meaning |
|---|---|---|
| unit_id | id | Unique unit serial |
| timestamp | datetime | End-of-line test time |
| lot_id | cat | Production lot (2-day lots per line) |
| production_line | cat | Assembly line |
| shift | cat | Day / Swing / Night |
| operator_id | cat | Line operator |
| die_bonder_id | cat | Die/wire bonding machine |
| tester_id | cat | End-of-line test station |
| product_family | cat | SLOTTED_SWITCH, REFLECTIVE_SENSOR, IR_EMITTER, PHOTOTRANSISTOR |
| part_number | cat | Fictional part number within family |
| led_die_supplier | cat | Supplier of LED die (empty if the unit has no LED) |
| detector_die_supplier | cat | Supplier of phototransistor die (empty if no detector) |
| mold_compound_batch | cat | Epoxy moulding compound batch |
| die_attach_temp_C | num | Die attach stage temperature |
| wire_bond_force_gf | num | Wire bond force, grams-force |
| ultrasonic_power_mW | num | Bonder ultrasonic power |
| cure_time_min, cure_temp_C | num | Epoxy cure profile |
| mold_pressure_MPa | num | Transfer moulding pressure |
| ambient_humidity_pct | num | Cleanroom relative humidity |
| particle_count_per_m3 | num | Cleanroom particle count |
| reflow_peak_temp | num | Reflow oven peak temperature (unit not stated — check it) |
| led_forward_voltage_V | num | LED Vf at test current |
| led_reverse_leakage_uA | num | LED reverse leakage |
| radiant_intensity_mW_sr | num | LED optical output |
| dark_current_nA | num | Phototransistor collector dark current |
| on_state_collector_current_mA | num | Collector current with LED on / target present |
| vce_saturation_V | num | Collector-emitter saturation voltage |
| rise_time_us, fall_time_us | num | Switching times |
| slot_alignment_offset_um | num | Emitter–detector optical axis offset (slotted switches only) |
| reflective_response_pct | num | Response at reference distance vs. golden unit (reflective sensors only) |
| xray_void_pct | num | Die-attach void area from X-ray |
| lead_coplanarity_um | num | Lead coplanarity |
| visual_crack_flag | 0/1 | Visual inspector saw a crack |
| visual_inspection_score | 1–5 | Inspector cosmetic score |
| burnin_drift_pct | num | Parameter drift after burn-in |
| rework_ticket_id | id | Rework system ticket |
| defect_type, is_defective | target | See above |
