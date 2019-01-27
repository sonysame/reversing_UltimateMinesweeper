# reversing_UltimateMinesweeper
#reversing_UltimateMinesweeper

The binary is .net strucure! So I use the tool, dnSpy.
```
private void SquareRevealedCallback(uint column, uint row)
{
	if (this.MineField.BombRevealed)
	{
		this.stopwatch.Stop();
		Application.DoEvents();
		Thread.Sleep(1000);
		new FailurePopup().ShowDialog();
		Application.Exit();
	}
	this.RevealedCells.Add(row * MainForm.VALLOC_NODE_LIMIT + column);
	if (this.MineField.TotalUnrevealedEmptySquares == 0)
	{
		this.stopwatch.Stop();
		Application.DoEvents();
		Thread.Sleep(1000);
		new SuccessPopup(this.GetKey(this.RevealedCells)).ShowDialog();
		Application.Exit();
	}
}
```

```
		// Token: 0x0600000D RID: 13 RVA: 0x000023E4 File Offset: 0x000005E4
		private string GetKey(List<uint> revealedCells)
		{
			revealedCells.Sort();
			Random random = new Random(Convert.ToInt32(revealedCells[0] << 20 | revealedCells[1] << 10 | revealedCells[2]));
			byte[] array = new byte[32];
			byte[] array2 = new byte[]
			{
				245,
				75,
				65,
				142,
				68,
				71,
				100,
				185,
				74,
				127,
				62,
				130,
				231,
				129,
				254,
				243,
				28,
				58,
				103,
				179,
				60,
				91,
				195,
				215,
				102,
				145,
				154,
				27,
				57,
				231,
				241,
				86
			};
			random.NextBytes(array);
			uint num = 0u;
			while ((ulong)num < (ulong)((long)array2.Length))
			{
				byte[] array3 = array2;
				uint num2 = num;
				array3[(int)num2] = (array3[(int)num2] ^ array[(int)num]);
				num += 1u;
			}
			return Encoding.ASCII.GetString(array2);
		}
```

```
		// Token: 0x17000009 RID: 9
		// (get) Token: 0x0600001E RID: 30 RVA: 0x00002BBC File Offset: 0x00000DBC
		public bool BombRevealed
		{
			get
			{
				int num = 0;
				while ((long)num < (long)((ulong)this.Size))
				{
					int num2 = 0;
					while ((long)num2 < (long)((ulong)this.Size))
					{
						if (this.MinesPresent[num2, num] && this.MinesVisible[num2, num])
						{
							return true;
						}
						num2++;
					}
					num++;
				}
				return false;
			}
		}
```
