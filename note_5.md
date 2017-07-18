* 对于tighten(row)的理解:

  new_row = [i for i in row if i != 0]
  new_row += [0 for i in range(len(row) - len(new_row))]
  
  因为是把所有非零单元统一归并到左边，所以 new_row = [i for i in row if i != 0] 就先把非零单元挑出并放在 new_row 这个列表中。
  非零单元都挑出来了，剩下的都是 0 了。所以 new_row += [0 for i in range(len(row) - len(new_row))] 就是完成填充 零单元的工作。
