import static org.hamcrest.CoreMatchers.is;
import static org.junit.Assert.assertThat;
import static org.junit.Assert.fail;
import org.junit.Before;
import org.junit.Test;

public class BankTest {
    private Bank bank;

    @Before
    public void setUp() {
        bank = new Bank();
    }

    @Test
    public void testInitialBalance() {
        assertThat(bank.getBalance(), is(0.0));
    }

    @Test
    public void testDeposit() {
        bank.deposit(100.0);
        assertThat(bank.getBalance(), is(100.0));
    }

    @Test
    public void testWithdraw() {
        bank.deposit(100.0);
        bank.withdraw(150.0);
        assertThat(bank.getBalance(), is(50.0));
    }

    @Test
    public void testWithdrawMoreThanBalance() {
        bank.deposit(100.0);
        try {
            bank.withdraw(150.0);
            fail("Should have thrown an exception");
        } catch (IllegalArgumentException e) {
            assertThat(e.getMessage(), is("Insufficient funds"));
        }
    }

    @Test
    public void testBalanceCheck() {
        bank.deposit(100.0);
        assertThat(bank.getBalance(), is(100.0));
    }
}
