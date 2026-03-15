  * ```javascript
  const date = new Date('2020-10-25T05:39:22.056Z')

  const orders = await prisma.order.findMany({
    where: {
      AND: [{ timeslot: { start: { lt: date } } }],
    },
    include: {
      timeslot: true,
      kitchenTickets: true,
      rsState: true,
      ocBinState: true,
    },
  })

  const updateOrders = await prisma.order.updateMany({
    where: { id: { in: orders.map((order) => order.id) } },
    data: { status: 'COMPLETE' },
  })

  console.log(updateOrders)

  // const filterout = orders.filter((entity) => entity.rsState.length)

  // console.log(filterout.map((entity) => entity.rsState))

  // const listofrs = orders.reduce((arr: any, entity) => {
  //   return [
  //     ...arr,
  //     ...entity.rsState.map((state) => state.id).filter((value) => value),
  //   ] as any
  // }, [])

  // console.log(listofrs)

  // const updateRsState = await prisma.orderRsState.updateMany({
  //   where: { id: { in: listofrs } },
  //   data: { status: 'SCANNED' },
  // })

  // console.log(updateRsState)

  // const listofoc = orders.reduce((arr: any, entity) => {
  //   return [
  //     ...arr,
  //     ...entity.ocBinState.map((state) => state.id).filter((value) => value),
  //   ] as any
  // }, [])

  // console.log(listofoc)

  // const updateOcBin = await prisma.orderOcBinState.updateMany({
  //   where: { id: { in: listofoc } },
  //   data: { status: 'DONE' },
  // })

  // console.log(updateOcBin)

  // const listOfIds = orders.reduce((arr: any, entity) => {
  //   return [
  //     ...arr,
  //     ...entity.kitchenTickets
  //       .map((ticket) => ticket.id)
  //       .filter((value) => value),
  //   ] as any[]
  // }, [])

  // console.dir(JSON.stringify(listOfIds))

  // const updateTickets = await prisma.kitchenTicket.updateMany({
  //   where: { id: { in: listOfIds } },
  //   data: { status: 'DONE' },
  // })

  // console.log(updateTickets)

  // const hello = await prisma.kitchenTicket.updateMany({
  //   data: { status: 'DONE' },
  //   where: {id: {in: }}
  // })

  // console.dir(
  //   JSON.stringify(
  //     orders
  //       .sort((a, b) =>
  //         new Date(a.timeslot.start) < new Date(b.timeslot.start) ? -1 : 1,
  //       )
  //       .map((entity) => ({
  //         ...entity,
  //         timeslot: {
  //           ...entity.timeslot,
  //           start: entity.timeslot.start.toUTCString(),
  //         },
  //       })),
  //   ),
  // )```
