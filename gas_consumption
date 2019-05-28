// py-evm which is a python Ethereum client written in Python lang.
// The code below is partially pasted from the total computation process. 

    #
    # Gas Consumption
    #
    def get_gas_meter(self) -> GasMeter:
        return GasMeter(self.msg.gas)

    def consume_gas(self, amount: int, reason: str) -> None:
        """
        Consume ``amount`` of gas from the remaining gas.
        Raise `eth.exceptions.OutOfGas` if there is not enough gas remaining.
        """
        return self._gas_meter.consume_gas(amount, reason)

    def return_gas(self, amount: int) -> None:
        """
        Return ``amount`` of gas to the available gas pool.
        """
        return self._gas_meter.return_gas(amount)

    def refund_gas(self, amount: int) -> None:
        """
        Add ``amount`` of gas to the pool of gas marked to be refunded.
        """
        return self._gas_meter.refund_gas(amount)

    def get_gas_refund(self) -> int:
        if self.is_error:
            return 0
        else:
            return self._gas_meter.gas_refunded + sum(c.get_gas_refund() for c in self.children)

    def get_gas_used(self) -> int:
        if self.should_burn_gas:
            return self.msg.gas
        else:
            return max(
                0,
                self.msg.gas - self._gas_meter.gas_remaining,
            )

    def get_gas_remaining(self) -> int:
        if self.should_burn_gas:
            return 0
        else:
