def logical_left_shift(binary_str, positions):
    """Perform logical left shift on an 8-bit binary string."""
    print(f"\n{'='*55}")
    print(f"LOGICAL LEFT SHIFT: {binary_str} << {positions}")
    print(f"{'='*55}")
    print(f"Original 8-bit number: {binary_str}")

    current = binary_str
    print(f"\nShifting step by step:")
    print(f"  Start : {current}")
    for i in range(1, positions + 1):
        # Drop leftmost bit, append 0 on the right
        shifted = current[1:] + '0'
        print(f"  Shift {i}: {shifted}   (drop leftmost bit '{current[0]}', append 0)")
        current = shifted

    # Final result guaranteed to be 8 bits
    final = current[-8:].zfill(8)
    print(f"\nFinal 8-bit result: {final}")
    print(f"Decimal value     : {int(final, 2)}")
    return final


def logical_right_shift(binary_str, positions):
    """Perform logical right shift on an 8-bit binary string."""
    print(f"\n{'='*55}")
    print(f"LOGICAL RIGHT SHIFT: {binary_str} >> {positions}")
    print(f"{'='*55}")
    print(f"Original 8-bit number: {binary_str}")

    current = binary_str
    print(f"\nShifting step by step:")
    print(f"  Start : {current}")
    for i in range(1, positions + 1):
        # Prepend 0 on the left, drop rightmost bit
        shifted = '0' + current[:-1]
        print(f"  Shift {i}: {shifted}   (prepend 0, drop rightmost bit '{current[-1]}')")
        current = shifted

    final = current[-8:].zfill(8)
    print(f"\nFinal 8-bit result: {final}")
    print(f"Decimal value     : {int(final, 2)}")
    return final


def verify(op_name, original, expected, actual):
    print(f"\n--- Verification: {op_name} ---")
    print(f"  Manual calculation : {expected}")
    print(f"  Program output     : {actual}")
    status = "PASS" if expected == actual else "FAIL"
    print(f"  Status             : {status}")
    return status == "PASS"


def main():
    # ---------- Operation (a): Logical Left Shift ----------
    a_original = "10110110"
    a_positions = 3
    a_actual = logical_left_shift(a_original, a_positions)

    # Manual calculation for left shift by 3:
    # 10110110 -> 01101100 -> 11011000 -> 10110000
    a_manual = "10110000"

    # ---------- Operation (b): Logical Right Shift ----------
    b_original = "11010100"
    b_positions = 3
    b_actual = logical_right_shift(b_original, b_positions)

    # Manual calculation for right shift by 3:
    # 11010100 -> 01101010 -> 00110101 -> 00011010
    b_manual = "00011010"

    # ---------- Verification ----------
    print(f"\n{'='*55}")
    print("FINAL VERIFICATION")
    print(f"{'='*55}")
    ok_a = verify("a) Left Shift by 3", a_original, a_manual, a_actual)
    ok_b = verify("b) Right Shift by 3", b_original, b_manual, b_actual)

    if ok_a and ok_b:
        print("\nAll operations verified successfully. ✔")
    else:
        print("\nVerification failed. ✘")


if __name__ == "__main__":
    main()
